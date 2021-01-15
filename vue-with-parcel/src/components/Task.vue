<template>
    <div class="container" style="margin-top:50px; margin-bottom: 50px;">
        <div class="row">
            <div class="col-md-3" style="margin-bottom: 20px; background-color: #bee5d3" v-for="category in categories" :key="category.id">
                <div class="card-header text-white" style="background-color: #00af91;">
                    {{ category.name }}
                </div>
                <div class="container overflow-auto" style="height: 90vh;">
                    <div class="row" style="margin-top: 5px; width: 35vh">
                        <TaskBody 
                            v-for="task in category.Tasks" :key="task.id" 
                            :dataTask="task" 
                            @editTask="editTask" 
                            :taskData="dataTask" 
                            @deleteTask="deleteTask" 
                            :categories="categories" 
                            @editCategory="editCategory" 
                            @taskEdit="taskEdit"/>
                    </div>
                </div>
            </div>    
        </div>
    </div>    
</template>

<script>
import TaskBody from './TaskBody'

export default {
    name: "Task",
    components: {
        TaskBody
    },
    props: ['categories', 'dataTask'],
    methods: {
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
    }
}
</script>

<style>

</style>