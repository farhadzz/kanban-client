<template>
  <div class="container" id='login-form' style="margin-top:150px">
    <div class="row g-0">
      <div class="col-sm-6 col-md-6 ">
        <div class="box-container">
          <div class="home-p" style="margin-left: 60px;">
            <div>
              <h3>Kanban Board</h3>
            </div>
            <div>
              <p>
                A Kanban board is a tool for workflow visualization and one of the Kanban method's key components.
                Visualizing your workflow and tasks on a  Kanban board helps you better understand your processes and gain 
                an overview of your workload. With this new level of transparency, you will quickly identify problematic work stages, 
                and by improving those, your team will soon work more efficiently. 
              </p>
            </div>
          </div>
        </div>
      </div>
      <form class="form-container" @submit.prevent="loginSubmit">
        <h3 class="login-p">Login</h3>
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Email address</label>
          <input type="email" class="form-control" aria-describedby="emailHelp" v-model="email">
          <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
        </div>
        <div class="mb-3">
          <label for="register-password" class="form-label">Password</label>
          <input type="password" class="form-control" v-model="password">
        </div>
        <button type="submit" class="btn btn-primary" id="login-btn" >Log In</button>
        <button class="btn btn-success" type="button" @click="registerButton">Register</button>
        <div>
          <br>
          <h5> or Sign in by Google</h5>
          <br>
        </div>
        <!-- <div class="g-signin2" data-onsuccess="onSignIn"></div> -->
      </form>
    </div>
  </div>
</template>

<script>
import Swal from "sweetalert2"

export default {
    name: "LoginForm",
    data() {
      return {
        email: '',
        password: ''
      }
    },
    methods: {
       loginSubmit(){
          const obj = {
            email: this.email, 
            password: this.password
          }
          if(!obj.email || !obj.password) {
          Swal.fire({
              icon: 'error',
              title: 'Oops...',
              text: 'Email and Password is required'
          })
        } else {
          // console.log(obj, "obj")
          return this.$emit('loginSubmit', obj)
        }
      },
      registerButton() {
        return this.$emit('registerButton')
      }
    }
}
</script>

<style>

</style>