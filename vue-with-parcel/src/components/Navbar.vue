<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container-fluid">
          <a class="navbar-brand" href="#" style="margin-left:30px">Kanban Board</a>
        </div>
          <!--  Sign Out & Add New Task Button-->
          <button class="btn btn-primary" type="submit" id="add-task-btn" style="margin-right: 20px; width: 180px;">Add New Task</button>
          <button class="btn btn-danger" type="submit" @click="signOut" style="margin-right: 30px; width: 150px;">Sign Out</button>
    </nav>
</template>

<script>
export default {
    name: "Navbar",
    methods: {
      signOut() {
        return this.$emit('signOut')
      }
    }
}
</script>

<style>

</style>