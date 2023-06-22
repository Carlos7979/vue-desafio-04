<script>
    import Header from './components/Header.vue'
    import Info from './components/Info.vue'
    import Table from './components/Table.vue'
    import Form from './components/Form.vue'
    const rows = [{ row: ['Nombre', 'Correo', 'Número', 'Password', 'Ciudad', 'Idiomas', 'Color'] }]

    export default {
        components: {
            Header,
            Info,
            Table,
            Form
        },
        data() {
            return {
                headerClass: {
                    'header-table': true,
                    'header-purple': false
                },
                rows,
                rowStyle: ['background: white', 'background: gray', '; background: gold'],
                horizontalView: false
            }
        },
        created() {},
        methods: {
            handleSubmit(data) {
                const row = [
                    data.name,
                    data.email,
                    data.number,
                    data.password,
                    data.city,
                    data.lang,
                    data.color
                ]
                this.rows.push({ row })
            },
            handleClick() {
                this.horizontalView = !this.horizontalView
            }
        },
        computed: {}
    }
</script>

<template>
    <div class="main">
        <Header></Header>
        <div :class="horizontalView ? 'horizontal' : ''">
            <div>
                <Info></Info>
                <hr v-show="!horizontalView" />
            </div>
            <button
                :class="`btn btn-secondary ${horizontalView ? ' button-h' : ' button'}`"
                @click="handleClick"
            >
                Cambiar vista
            </button>
            <Form @submit="handleSubmit"></Form>
            <Table
                :rows="rows"
                :row-style="rowStyle"
                table-title="Datos recolectados"
                :header-class="headerClass"
            ></Table>
        </div>
    </div>
</template>

<style scoped>
    .horizontal {
        display: flex;
        justify-content: space-around;
    }

	.button-h {
		height: fit-content;
		margin: 10px 40px;
	}

	.button {
		margin: 10px 45%;
	}
</style>
