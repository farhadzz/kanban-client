<template>
    <div class="container">
        <!-- Login -->
        <LoginForm 
            v-if="currentPage === 'login'" 
            @loginSubmit="login" 
            @registerButton="registerButton" 
            @loggedIn="loggedIn"
        ></LoginForm>
        <!-- Register -->
        <RegisterForm 
            v-else-if="currentPage === 'register'"
            @registerSubmit="register" 
            @cancel="cancelButton"
        ></RegisterForm>
        <!-- Home -->
        <Home v-else 
            :categories="categories" 
            @signOut="signOutButton" 
            @addTask="addTask" 
            @editTask="editTask" 
            :dataTask="dataTask" 
            @deleteTask="deleteTask" 
            @editCategory="editCategory" 
            @taskEdit="taskEdit"
        ></Home>
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
            url: 'https://server-kanban-farhad.herokuapp.com',
            categories: [],
            dataTask: {},
            
        }
    },
    components : {
        LoginForm,
        RegisterForm,
        Home
    },
    methods: {
        login(payload) {
            if(!payload.email || !payload.password) {
                Swal.fire({
                    icon: 'error',
                    title: 'Oops...',
                    text: 'Email and Password is required'
                })
            } else {
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
                    Swal.fire({
                        icon: 'error',
                        title: 'Oops...',
                        text: 'Invalid Email or Password'
                    })
                    console.log(err, "error di login")
                })
            }
            // console.log(payload, "pyayload")
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
        loggedIn() {
            this.fetchTask()
            this.currentPage = 'home'
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
                    Swal.fire({
                        icon: 'error',
                        title: 'Oops...',
                        text: 'Email is already used'
                    })
                    console.log(err, "dari register")
                })
        },
        addTask(payload) {
            // console.log(payload)
            axios({
                method: 'POST',
                url: this.url + '/tasks',
                data: {
                    name: payload.name,
                    description: payload.description
                },
                headers: {
                    access_token: localStorage.access_token
                }
            })
                .then(data => {
                    this.fetchTask()
                    this.currentPage = "home"
                })
                .catch(err => {
                    
                    console.log(err, "error di add")
                })
        },
        deleteTask(payload) {
            axios({
                method: 'DELETE',
                url: this.url + '/tasks/' + payload.id,
                headers: {
                    access_token: localStorage.access_token
                }
            })
                .then(data => {
                    this.fetchTask()
                    this.currentPage = 'home'
                })
                .catch(err => {
                    console.log(err, 'error di delete')
                })
        },
        editTask(payload) {
            console.log(payload, "editTask")
            this.dataTask = payload
        },
        taskEdit(payload){
            axios({
                method: 'PUT',
                url: this.url + '/tasks/' + this.dataTask.id,
                headers: {
                    access_token: localStorage.access_token
                },
                data: {
                    name: payload.name,
                    description: payload.description
                }
            })
                .then(data=> {
                    this.fetchTask()
                    this.currentPage = 'home'
                })
                .catch(err => {
                    console.log(err, 'error di edit')
                })
        },
        editCategory(payload) { 
            axios({
                method: 'PATCH',
                url: this.url + '/tasks/' + payload.id,
                headers: {
                    access_token: localStorage.access_token
                },
                data: {
                    CategoryId: payload.CategoryId
                }
            })
                .then(data => {
                    this.fetchTask()
                    this.currentPage = 'home'
                })
                .catch(err => {
                    console.log(err, 'error di edit category')
                })
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
        },
        signOut() {
            const auth2 = gapi.auth2.getAuthInstance();
            auth2.signOut().then(function () {
                console.log('User signed out');
        });
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