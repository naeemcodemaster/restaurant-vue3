<template>
    <div>
        <img src="../assets/logo.jpg" />
        <ul v-for="error in errors" v-bind:key="error">
            <li>
                {{ error }} is required
            </li>
        </ul>
        <div class="register">
            <input type="text" placeholder="Enter Email" v-model="form.email" />
            <input type="password" placeholder="Enter Password" v-model="form.password" />
            <button v-on:click="login">Login</button>
            <p id="loginlink">
                Don't have an account <router-link to="/signup">Sign Up</router-link>
            </p>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    name: 'SignUp',
    data() {
        return {
            form: {
                email: '',
                password: '',
            },
            errors: []
        }
    },
    methods: {
        async login() {
            this.errors = [];
            for (const field in this.form) {
                if (this.form[field] === "" || this.form[field].length === 0) {
                    this.errors.push(field);

                }
            }

            if (this.errors.length === 0) {
                let result = await axios.get(`http://localhost:3000/user?email=${this.form.email}&password=${this.form.password}`);
                console.log(result);
                if (result.status == 200 && result.data.length > 0) {
                    // alert('Sign Up has been successfully');
                    localStorage.setItem('user-info', JSON.stringify(result.data));
                    this.$router.push({ name: 'HomePage' })
                } else {
                    console.log("Not Login")
                    alert('Invalid Credentials')
                }
            }

        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        console.log(user);
        if (user) {
            this.$router.push({ name: 'HomePage' })
        }
    }
}

</script>
<style scoped>
img {
    width: 100px;
}

.register input {
    width: 300px;
    height: 35px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-right: auto;
    margin-left: auto;
    border-radius: 5px;
    border: 1px solid #c3c3c3;
    font-size: 12px;
    color: #7c7b7b;
}

.register button {
    width: 320px;
    height: 40px;
    background: #FFC200;
    color: #fff;
    border: none;
    border-radius: 5px;
}

.register button:hover {
    background-color: #c79c0e;
    cursor: pointer;
}

ul li {
    color: red;
    list-style: none;
}

#loginlink {
    width: 320px;
    margin: 0 auto;
    margin-top: 10px;

}

#loginlink a {
    color: #17708b;
    font-size: 15px;



}</style>