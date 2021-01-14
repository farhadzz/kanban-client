<template>
    <div class="container" style="margin-top:50px; margin-bottom: 50px;">
        <div class="row">
            <div class="col-md-3" style="margin-bottom: 20px" v-for="category in categories" :key="category.id">
                <div class="card-header text-white" style="background-color: #00af91;">
                    {{ category.name }}
                </div>
                <div class="container overflow-auto" style="height: 85vh">
                    <div class="row" style="margin-top: 5px;">
                        <TaskBody v-for="task in category.Tasks" :key="task.id" :dataTask="task"/>
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
    props: ['categories']
}
</script>

<style>

</style>