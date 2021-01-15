<template>
  <!-- Button trigger modal -->
  <div>

<!-- Modal -->
  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Add New Task</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="addTask">
          <div class="mb-3">
            <label for="recipient-name" class="col-form-label">Title:</label>
            <input type="text" class="form-control"  v-model="name">
          </div>
          <div class="mb-3">
            <label for="message-text" class="col-form-label" >Description:</label>
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
import Swal from 'sweetalert2'

export default {
    name: "ModalAdd",
    data() {
      return {
        name: '',
        description: ''
      }
    },
    methods: {
      addTask() {
        
        let obj = { 
          name: this.name,
          description: this.description
        }
        if(!obj.name || !obj.description) {
          Swal.fire({
              icon: 'error',
              title: 'Oops...',
              text: 'Form must be filled'
          })
        } else {
          return this.$emit('addTask', obj)
        }
      }
    }

}
</script>

<style>

</style>