<script>
    import Header from './components/Header.vue'
    import Info from './components/Info.vue'
    import Table from './components/Table.vue'

    const rows = [
        { row: ['Nombre', 'Correo', 'Número', 'Password', 'Ciudad'] },
        { row: ['Carlos', 'carlos@email.com', 20, 123, 'Caracas'] }
    ]

    export default {
        components: {
            Header,
            Info,
            Table
        },
        data() {
            return {
                headerClass: {
                    'header-table': true,
                    'header-purple': false
                },
                rows,
                rowStyle: ['background: white', 'background: gray', '; background: gold']
            }
        },
        created() {},
        methods: {},
        computed: {}
    }
</script>

<template>
	<div class="main">
		<Header></Header>
        <Info></Info>
        <hr />
        <Table
            :rows="rows"
            :row-style="rowStyle"
            table-title="Tabla 1"
            :header-class="headerClass"
        ></Table>
    </div>
</template>

<style scoped></style>
