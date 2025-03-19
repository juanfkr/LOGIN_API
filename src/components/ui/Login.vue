<template>
    <div class="login-form">
        <h2>Login</h2>
        <input type="text" v-model="username" placeholder="Insira sua senha">
        <input type="text" v-model="password" placeholder="Insira seu nome de usuário">
        <button @click="loginUser">Acessar</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const username = ref('');
const password = ref('');

async function loginUser() {
    try {
        const response = await fetch('http://localhost:3000/users')
        const data = await response.json();
        
        // Usando find para localizar o usuário correto
        const foundUser = data.find(user => 
            user.name === username.value && user.password === password.value
        );
        
        if (foundUser) {
            alert('login realizado');
        } else {
            alert('seu nome ou senha está errado');
        }
    } catch(e) {
        console.log(e.message)
    }
}
</script>

<style scoped>
.login-form {
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