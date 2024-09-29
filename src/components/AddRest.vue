<template lang="">
    <div>
        <h2>Add New Restaurant</h2>
        <ul v-for="error in errors" v-bind:key="error">
            <li>
                {{ error }} is required
            </li>
        </ul>
        <form>
            <input type="text" name="name" placeholder="Enter Name" v-model="restform.name"/>
            <input type="text" name="contact" placeholder="Enter Contact" v-model="restform.contact"/>
            <input type="text" name="address" placeholder="Enter Address" v-model="restform.address"/>
            <button type="button" @click="addRestFun">Add Restaurant</button>

        </form>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    name: 'AddRest',
    data() {
        return {
            restform: {
                name: '',
                contact: '',
                address: ''
            },
            errors: []
        }
    },
    methods:{
        async addRestFun(){
            this.errors = [];
            for (const field in this.restform) {
                if (this.restform[field] === "" || this.restform[field].length === 0) {
                    this.errors.push(field);

                }
            }
            console.log(this.restform)
            if (this.errors.length === 0) {
            const result = await axios.post('http://localhost:3000/restaurant',{
                name:this.restform.name,
                contact:this.restform.contact,
                address:this.restform.address
            })
            console.log(result);
            this.$router.push('/')

        }
        }
    },
    async mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({ name: 'LoginPage' });
        }
        
       
        

    },
}
</script>
<style scoped>
h2 {
    margin-top: 20px;
    margin-bottom: 10px;
}

input {
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

button {
    width: 320px;
    height: 40px;
    background: #FFC200;
    color: #fff;
    border: none;
    border-radius: 5px;
}

button:hover {
    background-color: #c79c0e;
    cursor: pointer;
}
ul li{
    color: red;
    list-style: none;
}
</style>