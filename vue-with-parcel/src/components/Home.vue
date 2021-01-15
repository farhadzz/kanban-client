<template>
    <div>
    <!-- Navbar -->
        <div>
            <Navbar 
                @signOut="signOut" 
                @addTask="addTask"
            ></Navbar>
        </div>
    <!--  Task -->
        <div>
            <Task 
                :categories="categories" 
                @editTask="editTask" 
                :dataTask="dataTask" 
                @deleteTask="deleteTask" 
                @editCategory="editCategory" 
                @taskEdit="taskEdit"/>    
        </div>
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
    props: [ 'categories', 'dataTask' ],
    methods: {
        signOut() {
            return this.$emit('signOut')
        },
        addTask(obj) {
            return this.$emit('addTask',obj)
        },
        editTask(dataTask) {
            return this.$emit('editTask', dataTask)
        },
        deleteTask(obj) {
            return this.$emit('deleteTask', obj)
        },
        editCategory(obj) {
            return this.$emit('editCategory', obj)
        },
        taskEdit(obj) {
            return this.$emit('taskEdit', obj)
        }
    },
    created() {
        // console.log(this.categories)
    }
}
</script>

<style>

</style>