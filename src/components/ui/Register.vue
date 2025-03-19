<template>
    <div class="register-form">
        <h2>Registro</h2>
        <input type="text" v-model="userName" placeholder="Insira seu nome de usuário">
        <p v-if="!userName" class="emptyField">{{ emptyFieldMessage }}</p>
        <input type="text" v-model="userPassword" placeholder="Insira sua senha">
        <p v-if="!userPassword" class="emptyField">{{ emptyFieldMessage }}</p>
        <input type="text" v-model="confirmPassword" placeholder="Confirme sua senha">
        <p v-if="!confirmPassword" class="emptyField">{{ emptyFieldMessage }}</p>
        <button :disabled="!userName || !userPassword || !confirmPassword" @click="registerUser">Registrar-se</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const userName = ref('');
const userPassword = ref('');
const confirmPassword = ref('');
const emptyFieldMessage = 'Campo em branco'

function registerUser() {
    if (userPassword.value === confirmPassword.value) {
        setUser(userName.value, userPassword.value);
        clearForm(userName, userPassword, confirmPassword);
        return;
    }
    alert('as senhas não correspondem')
}

async function setUser(username, password) {
    try {
        const response = await fetch(`http://localhost:3000/users?name=${username}`);
        const data = await response.json();

        if (data.length > 0) {
            alert('usuário já existe');
            return;
        }
        alert('usuário criado');
        return await fetch('http://localhost:3000/users', {
            method: "POST",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify({
                name: username,
                password: password
            })
        })
    } catch (e) {
        alert(e)
    }
}

function clearForm(...inputs) {
    inputs.forEach(input => input.value = '');
}

</script>

<style scoped>
.register-form {
    display: flex;
    flex-direction: column;
    gap: .5em;
    margin-top: 2em;
    background-color: white;
    box-shadow: 0 .25em 1em rgba(0, 0, 0, 0.3);
    padding: 1em;
    border-radius: .5em;

    h2 {
        color: var(--default);
    }

    input {
        padding: .5em;
        border-radius: .5em;
        border: 1px solid rgba(0, 0, 0, 0.3);

        &:focus {
            outline: 1px solid var(--default);
        }
    }

    button {
        padding: .5em;
        border: none;
        border-radius: .5em;
        background-color: var(--default);
        color: white;
        transition: all .1s ease-in-out;

        &:active {
            opacity: 90%;
        }
    }
}

.emptyField {
    color: red;
    font-size: .8em;
}
</style>