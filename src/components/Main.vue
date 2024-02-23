<template>
    <main class="container">
        <Formulario @user-updated="updateUser"></Formulario>
        <Card :user="user"></Card>
    </main>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    gap: 30px;
}
</style>

<script>
import Card from './Card.vue';
import Formulario from './Formulario.vue';

export default {
    name: 'Main',
    data() {
        return {
            user: {
                nome: '',
                sobrenome: '',
                image: null
            }
        };
    },
    methods: {
        updateUser(userData) {
            this.user = userData;
        }
    },
    components: { Formulario, Card },
};
</script>