<template lang="">
    <div>
        <h2>Update Restaurant</h2>
        <form>
            <input type="text" name="name" placeholder="Enter Name" v-model="restaurant.name"/>
            <input type="text" name="contact" placeholder="Enter Contact" v-model="restaurant.contact"/>
            <input type="text" name="address" placeholder="Enter Address" v-model="restaurant.address"/>
            <button type="button" @click="addRestFun">Update Restaurant</button>

        </form>
    </div>
</template>
<script>
import axios from 'axios';
export default {
    name: 'UpdateRest',
    data() {
        return {
            restaurant: {
                name: '',
                contact: '',
                address: ''
            }
        }
    },
  
    methods:{
        async addRestFun(){
            console.log(this.restaurant)
            const result = await axios.put(`http://localhost:3000/restaurant/${this.$route.params.id}`,{
                name:this.restaurant.name,
                contact:this.restaurant.contact,
                address:this.restaurant.address
            })
            console.log(result);
            this.$router.push('/')
        }
    },
    async mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({ name: 'LoginPage' });
        }
        const id = this.$route.params.id;
        let result = await axios.get(`http://localhost:3000/restaurant/${id}`);
        console.log(result);
        this.restaurant = result.data;
        

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
</style>