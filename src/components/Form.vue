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
                errors: [],
                cities: ['', 'Caracas', 'Buenos Aires', 'Bogotá']
            }
        },
        created() {},
        mounted() {},
        methods: {
            handleSubmit() {
                if (this.validate()) {
                    this.$emit('submit', this.form)
                    this.resetForm()
                }
            },
            validate() {
                this.errors = []
                const form = this.form
                for (const input in form) {
                    if ((input === 'lang' && form[input].length === 0) || form[input] === '') {
                        this.$refs[input].focus()
                        this.$refs[input].classList.add('shadow')
                        this.errors.push('Todos los campos son obligatorios')
                        return false
                    } else {
                        this.$refs[input].classList.remove('shadow')
                    }
                }
                if (!this.emailValidate(form.email)) {
                    this.$refs['email'].focus()
                    this.$refs['email'].classList.add('shadow')
                    this.errors.push(`${form.email} no es un email válido`)
                    return false
                }
                this.errors = []
                return true
            },
            emailValidate(email) {
                const re = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/
                if (!re.test(String(email))) return false
                return true
            },
            resetForm() {
                this.form = {
                    name: '',
                    email: '',
                    number: '',
                    password: '',
                    city: '',
                    lang: [],
                    color: ''
                }
            }
        },
        computed: {},
        watch: {
            'form.name'(newValue, oldValue) {
                if (newValue && !oldValue) this.$refs['name'].classList.remove('shadow')
            },
            'form.email'(newValue, oldValue) {
                if (newValue && !oldValue) {
                    this.$refs['email'].classList.remove('shadow')
                    return
                }
                if (this.emailValidate(newValue)) {
                    this.$refs['email'].classList.remove('shadow')
                    this.validate()
                }
            },
            'form.number'(newValue, oldValue) {
                if (newValue && !oldValue) this.$refs['number'].classList.remove('shadow')
            },
            'form.password'(newValue, oldValue) {
                if (newValue && !oldValue) this.$refs['password'].classList.remove('shadow')
            },
            'form.city'(newValue, oldValue) {
                if (newValue && !oldValue) this.$refs['city'].classList.remove('shadow')
            },
            'form.lang.length'(newValue, oldValue) {
                if (newValue && !oldValue) this.$refs['lang'].classList.remove('shadow')
            },
            'form.color'(newValue, oldValue) {
                if (newValue && !oldValue) this.$refs['color'].classList.remove('shadow')
            }
        }
    }
</script>

<template>
    <div class="form-container">
        <form ref="form" action="" method="post" class="form">
            <div class="input-group-text">
                <label for="name">Nombre</label>
                <input
                    ref="name"
                    class="form-control"
                    v-model.trim="form.name"
                    type="text"
                    name="name"
                    id="name"
                />
            </div>
            <div class="input-group-text">
                <label for="email">Correo</label>
                <input
                    ref="email"
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
                    ref="number"
                    class="form-control"
                    v-model.prevent="form.number"
                    type="number"
                    name="number"
                    id="number"
                />
            </div>
            <div class="input-group-text">
                <label for="password">Contraseña</label>
                <input
                    ref="password"
                    class="form-control"
                    v-model="form.password"
                    type="password"
                    name="password"
                    id="password"
                />
            </div>
            <div class="input-group-text">
                <label for="city">Ciudad</label>
                <select ref="city" class="custom-select select" v-model="form.city" id="city">
                    <option v-for="(city, i) in cities" :key="`${i}-cities`" :value="city">
                        {{ city }}
                    </option>
                </select>
            </div>
            <div class="input-group-text">
                <label>Idiomas</label>
                <div ref="lang" class="form-control">
                    <label for="es">Español</label>
                    <input type="checkbox" name="lang" id="es" value="es" v-model="form.lang" />
                    <label for="en">Inglés</label>
                    <input type="checkbox" name="lang" id="en" value="en" v-model="form.lang" />
                </div>
            </div>
            <div class="input-group-text">
                <label>Color</label>
                <div ref="color" class="form-control">
                    <label for="blue">Azul</label>
                    <input type="radio" name="color" id="blue" value="azul" v-model="form.color" />
                    <label for="green">Verde</label>
                    <input
                        type="radio"
                        name="color"
                        id="green"
                        value="verde"
                        v-model="form.color"
                    />
                </div>
            </div>
            <input @click.prevent="handleSubmit" type="submit" value="Enviar" />
            <div
                v-show="errors.length > 0"
                class="alert alert-danger"
                v-for="(error, i) in errors"
                :key="`${i}-error`"
            >
                {{ error }}
            </div>
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
    .shadow {
        box-shadow: 1px 1px 1px 1px red !important;
    }
</style>
