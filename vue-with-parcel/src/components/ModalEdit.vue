<template>
    <div>
        <!-- Modal -->
        <div class="modal fade" id="editModal" tabindex="-1" aria-labelledby="editModalLabel" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="editModalLabel">Edit Task</h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        <form @submit.prevent="taskEdit">
                            <div class="mb-3">
                                <label for="recipient-name" class="col-form-label">Title:</label>
                                <input type="text" class="form-control" v-model="name">
                            </div>
                            <div class="mb-3">
                                <label for="message-text" class="col-form-label">Description:</label>
                                <textarea class="form-control" v-model="description"></textarea>
                            </div>
                            <button type="submit" class="btn btn-primary">Save changes</button>
                            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
</template>

<script>
    export default {
        name: "ModalEdit",
        props: ['taskData'],
        data() {
            return {
                name: '',
                description: ''
            }
        },
        methods: {
            deleteTask() {
                return this.$emit('deleteTask')
            },
            taskEdit() {
                let obj = {
                    name: this.name,
                    description: this.description
                }
                return this.$emit('taskEdit', obj)
            }
        },
        created() {
            // console.log(this.taskData)
            this.name = this.taskData.name
            this.description = this.taskData.description
        }
    }
</script>

<style>

</style>