<template>
    <div class="register-form">
        <h2>Registro</h2>
        <input type="text" v-model="userName" placeholder="Insira seu nome de usuário">
        <input type="text" v-model="userPassword" placeholder="Insira sua senha">
        <input type="text" v-model="confirmPassword" placeholder="Confirme sua senha">
        <button @click="registerUser">Registrar-se</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const userName = ref('');
const userPassword = ref('');
const confirmPassword = ref('');

function registerUser() {
    if (userPassword.value === confirmPassword.value) {
        setUser();
        clearForm(userName, userPassword, confirmPassword);
        alert('usuário criado');
        return;
    }
    alert('as senhas não correspondem')
}

async function setUser() {
    try {
        return await fetch('http://localhost:3000/users', {
            method: "POST",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify({
                name: userName.value,
                password: userPassword.value
            })
        })
    } catch (e) {
        alert(e)
    }
}

function clearForm(...args) {
    args.forEach((arg) => {
        arg.value = '';
    })
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
</style>