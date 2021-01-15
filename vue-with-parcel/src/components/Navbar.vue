<template>
<div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container-fluid">
          <a class="navbar-brand" href="#" style="margin-left:30px">Kanban Board</a>
        </div>
          <!--  Sign Out & Add New Task Button-->
          <button class="btn btn-primary" type="submit" id="add-task-btn" style="margin-right: 20px; width: 180px;" data-bs-toggle="modal" data-bs-target="#exampleModal">Add New Task</button>
          <button class="btn btn-danger" type="submit" @click.prevent="signOut" style="margin-right: 30px; width: 150px;">Sign Out</button>
    </nav>
    <ModalAdd @addTask="addTask">
</div>
</template>

<script>
import ModalAdd from './ModalAdd.vue'

export default {
    components: { 
    ModalAdd 
    },
    name: "Navbar",
    data() {
      return {
        name: '',
        description: ''
      }
    },
    methods: {
      signOut() {
        return this.$emit('signOut')
      },
      addTask(obj) {
        
        return this.$emit('addTask', obj)
      }
    }
}
</script>

<style>

</style>