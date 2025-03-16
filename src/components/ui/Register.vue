<template>
    <div class="register-form">
        <h2>Registro</h2>
        <input type="text" name="" id="" placeholder="Insira seu nome de usuário">
        <input type="text" name="" id="" placeholder="Insira sua senha">
        <input type="text" name="" id="" placeholder="Confirme sua senha">
        <button>Registrar-se</button>
    </div>
</template>

<script setup>

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