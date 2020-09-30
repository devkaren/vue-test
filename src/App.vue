<template>
    <div id="app">
        <h2>Task 1</h2>
        <hr/>
        <PriceTable/>
        <hr/>
        <br/>
        <br/>
        <br/>
        <br/>
        <h2>Task 2</h2>
        <hr/>
        <CarTable/>
    </div>
</template>

<script>
    import PriceTable from './components/PriceTable.vue'
    import CarTable from './components/CarTable.vue'

    export default {
        name: 'App',
        components: {
            PriceTable,
            CarTable
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
