<script>
    export default {
        name: 'Form',
        emits: ['submit'],
        mixins: [],
        components: {},
        props: {},
        data() {
            return {
                form: {
                    name: '',
                    email: '',
                    number: '',
                    password: '',
                    city: '',
                    lang: [],
                    color: ''
                },
                cities: ['', 'Caracas', 'Buenos Aires', 'Bogotá']
            }
        },
        created() {},
        mounted() {},
        methods: {
            handleSubmit() {
                this.$emit('submit', this.form)
            }
        },
        computed: {},
        watcher: {}
    }
</script>

<template>
    <div class="form-container">
        <form action="" method="post" class="form">
            <div class="input-group-text">
                <label for="name">Nombre</label>
                <input class="form-control" v-model.trim="form.name" type="text" name="name" id="name" />
            </div>
            <div class="input-group-text">
                <label for="email">Correo</label>
                <input
                    class="form-control"
                    v-model="form.email"
                    type="email"
                    name="email"
                    id="email"
                />
            </div>
            <div class="input-group-text">
                <label for="number">Número</label>
                <input
                    class="form-control"
                    v-model.number="form.number"
                    type="number"
                    name="number"
                    id="number"
                />
            </div>
            <div class="input-group-text">
                <label for="password">Contraseña</label>
                <input
                    class="form-control"
                    v-model="form.password"
                    type="password"
                    name="password"
                    id="password"
                />
            </div>
            <div class="input-group-text">
                <label for="city">Ciudad</label>
                <select class="custom-select select" v-model="form.city" id="city">
                    <option v-for="(city, i) in cities" :key="`${i}-cities`" :value="city">
                        {{ city }}
                    </option>
                </select>
            </div>
            <div class="input-group-text">
                <label>Idiomas</label>
                <div class="form-control">
                    <label for="es">Español</label>
                    <input type="checkbox" name="lang" id="es" value="es" v-model="form.lang" />
                    <label for="en">Inglés</label>
                    <input type="checkbox" name="lang" id="en" value="en" v-model="form.lang" />
                </div>
            </div>
            <div class="input-group-text">
				<label>Color</label>
                <div class="form-control">
					<label for="blue">Azul</label>
					<input type="radio" name="color" id="blue" value="azul" v-model="form.color" />
					<label for="green">Verde</label>
					<input type="radio" name="color" id="green" value="verde" v-model="form.color" />
				</div>
            </div>
            <input @click.prevent="handleSubmit" type="submit" value="Enviar" />
			<div class="alert alert-danger"></div>
        </form>
    </div>
</template>

<style scoped>
    .form-container {
        display: flex;
        justify-content: center;
    }

    .form {
        display: flex;
        flex-direction: column;
    }

    .select {
        width: 100%;
    }

    .input-group-text label {
        width: 7rem;
        text-align: end;
        font-weight: 600;
        margin-right: 5px;
    }

</style>
