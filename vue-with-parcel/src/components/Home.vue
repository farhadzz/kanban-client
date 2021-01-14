<template>
    <div>
    <!-- Navbar -->
        <Navbar @signOut="signOut"></Navbar>
    <!--  Task -->
        <Task :categories="categories"/>    
    </div>
</template>

<script>
import Navbar from "./Navbar"
import Task from "./Task"

export default {
    name: 'Home',
    components: {
        Navbar,
        Task
    },
    props: [ 'categories' ],
    methods: {
        signOut() {
            return this.$emit('signOut')
        }
    },
    created() {
        // console.log(this.categories)
    }
}
</script>

<style>

</style>