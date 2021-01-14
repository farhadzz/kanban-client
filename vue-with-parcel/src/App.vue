<template>
    <div class="container">
        <!-- Login -->
        <LoginForm v-if="currentPage === 'login'" @loginSubmit="login" @registerButton="registerButton"></LoginForm>
        <!-- Register -->
        <RegisterForm v-else-if="currentPage === 'register'" @registerSubmit="register" @cancel="cancelButton"></RegisterForm>
        <!-- Home -->
        <Home v-else :categories="categories" @signOut="signOutButton"></Home>
    </div>
</template>

<script>
import axios from "axios"
import Swal from "sweetalert2"
import LoginForm from "./components/LoginForm.vue"
import RegisterForm from "./components/RegisterForm.vue"
import Home from "./components/Home.vue"

export default {
    name: "App",
    data() {
        return {
            message: 'Hello World',
            currentPage: 'register',
            url: 'http://localhost:4000',
            categories: []
        }
    },
    components : {
        LoginForm,
        RegisterForm,
        Home
    },
    methods: {
        login(payload) {
            // console.log(payload, "pyayload")
            axios({
                method: 'POST',
                url: this.url + '/login',
                data: {
                    email: payload.email,
                    password: payload.password
                }
            })
            .then(({data: {
                access_token
            }}) => {
                // console.log(res, "vue"
               localStorage.setItem('access_token', access_token)
                // console.log(access_token)
                this.currentPage = "home"
                this.fetchTask()
            })
            .catch(err => {
                console.log(err, "error di login")
            })
        },
        fetchTask() {
            axios({
                method: "GET",
                url: this.url + "/categories",
                headers: {
                    access_token: localStorage.access_token
                }
            })
            .then(res => {
                // console.log(res)
                this.categories = res.data
                this.currentPage = "home"
            })
            .catch(err => {
                console.log(err, "dari fetch")
            })
        },
        register(payload) {
            // console.log(payload)
            axios({
                method: 'POST',
                url: this.url + '/register',
                data: {
                    name: payload.name,
                    email: payload.email,
                    password: payload.password
                }
            })
                .then(data => {
                    this.currentPage = "login"
                })
                .catch(err => {
                    console.log(err, "dari register")
                })
        },
        addTask(payload) {
            axios({
                method: 'POST',
                url: this.url + '/tasks',
                data: {
                    name: payload.name,
                    description: payload.description,
                    UserId: payload.UserId
                }
            })
                .then(data => {
                    this.fetchTask()
                    this.currentPage = "home"
                })
        },
        deleteTask(payload) {
            
        },
        patchTask(payload) {

        },
        addCategory(payload) {
            
        },
        cancelButton() {
            this.currentPage = "login"
        },
        registerButton() {
            this.currentPage = "register"
        },
        signOutButton() {
            localStorage.clear()
            this.currentPage = "login"
        }
    },
    created() {
        if(localStorage.access_token) {
            this.fetchTask()
            this.currentPage = "home"
        } else {
            localStorage.clear()
            this.currentPage = "login"
        }
    }
}
</script>

<style scoped>

</style>