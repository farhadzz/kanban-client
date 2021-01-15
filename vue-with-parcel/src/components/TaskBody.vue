<template>
    <div class="w-100" style="margin-bottom: 10px">
        <div class="card">
            <div class="card-body" style= "background-color: #d6b0b1">
                <h5 class="card-title">{{ dataTask.name }}</h5>
            </div>
            <ul class="list-group list-group-flush">
                <li class="list-group-item">{{ dataTask.description }}</li>
            </ul>
            <div class="card-body">
                <a href="#" class="card-link btn btn-outline-warning" data-bs-toggle="modal" data-bs-target="#editModal" @click.prevent="editTask">Update</a>
                <button type="button" class="btn btn-danger" @click.prevent="deleteTask">Delete</button>
                <div>
                    <label for="category" style="margin-top: 10px">Move task</label>
                    <form @submit.prevent="editCategory">
                        <select name="category" v-model="CategoryId">
                            <option 
                            v-for="category in categories" :key="category.id" 
                            v-bind:value="category.id">
                                {{ category.name }}
                            </option>
                        </select>
                        <button type="submit" class="btn btn-primary">Submit</button>
                    </form>
                </div>
            </div>
            <modal-edit :taskData="taskData" @taskEdit="taskEdit">
        </div>
    </div>
</template>

<script>
    import ModalEdit from './ModalEdit'

    export default {
        components: {
            ModalEdit,
        },
        data() {
            return {
                CategoryId: 0
            }
        },
        name: "TaskBody",
        props: ['dataTask', 'taskData', 'categories'],
        methods: {
            editTask() {
                return this.$emit('editTask', this.dataTask)
            },
            deleteTask() {
                let obj = {
                    id: this.dataTask.id
                }
                return this.$emit('deleteTask', obj)
            },
            editCategory() {
                let obj = {
                    CategoryId: this.CategoryId,
                    id: this.dataTask.id
                }    
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