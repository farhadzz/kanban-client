<template>
  <div>
  <div class="container" id="register-form" style="margin-top:150px">
    <div class="row g-0">
      <div class="col-sm-6 col-md-6 ">
        <div class="box-container">
          <div class="home-p" style="margin-left: 60px;">
            <div>
              <h3>Kanban Board</h3>
            </div>
            <p>
              A Kanban board is a tool for workflow visualization and one of the Kanban method's key components.
                Visualizing your workflow and tasks on a  Kanban board helps you better understand your processes and gain 
                an overview of your workload. With this new level of transparency, you will quickly identify problematic work stages, 
                and by improving those, your team will soon work more efficiently. 
            </p>
          </div>

        </div>
      </div>
      <form class="form-container" @submit.prevent="registerSubmit">
        <h3 class="register-p">Register</h3>
        <div class="mb-3">
          <label for="name-register" class="form-label">Name</label>
          <input type="text" class="form-control" aria-describedby="emailHelp" v-model="name">
        </div>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Email address</label>
          <input type="email" class="form-control" aria-describedby="emailHelp" v-model="email">
          <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
        </div>
        <div class="mb-3">
          <label for="exampleInputPassword1" class="form-label">Password</label>
          <input type="password" class="form-control" v-model="password">
        </div>
        <div class="col-auto">
          <button class="btn btn-danger" type="submit" id='register-submit'>Register</button>
          <button class="btn btn-secondary" type="button" @click="cancel">Cancel</button>
        </div>
      </form>
    </div>
  </div>
</div>
</template>

<script>
import Swal from "sweetalert2"

export default {
    name: "RegisterForm",
    data() {
      return {
        name: '',
        email: '',
        password: ''
      }
    },
    methods: {
      registerSubmit() {
        const obj = {
          name: this.name,
          email: this.email,
          password: this.password
        }
        if(!obj.name || !obj.email || !obj.password) {
          Swal.fire({
              icon: 'error',
              title: 'Oops...',
              text: 'Name, Email and Password is required'
          })
        } else {
          return this.$emit('registerSubmit', obj)
        }
        // console.log(obj, "form")
      },
      cancel() {
        return this.$emit('cancel')
      }
    }

}
</script>

<style>

</style>