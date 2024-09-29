<template>
    <div>
        <h3>Welcome, {{ username }}</h3>
        <table border="1">
            <tr>
                <th>Name</th>
                <th>Contact</th>
                <th>Address</th>
                <th>Edit</th>
                <th>Delete</th>
            </tr>
            <tr v-for="item in restaurant" :key="item.id">
                <td>{{ item.name }}</td>
                <td>{{ item.contact }}</td>
                <td>{{ item.address }}</td>
                <td class="editBtn"><router-link :to="'/update/' + item.id">Edit</router-link></td>
                <td><button class="deleteBtn" @click="deleteRest(item.id)">Delete</button></td>
            </tr>
        </table>
    </div>
</template>
<script>

import axios from 'axios';
export default {
    name: 'HomePage',
    data() {
        return {
            username: '',
            restaurant: [],
        }
    },
    methods: {
        async deleteRest(id) {
            let result = await axios.delete(`http://localhost:3000/restaurant/${id}`);
            console.log(result);
            if (result.status == 200) {
                this.loadData();
            }
        },
        async loadData() {
            
            let user = localStorage.getItem('user-info');
            if (user) {
                let parseUser = JSON.parse(user); // Parse the array from localStorage
                if (Array.isArray(parseUser) && parseUser.length > 0) {
                    this.username = parseUser[0].name; // Access the 'name' from the first object in the array
                    console.log(this.username); // Should print "majid"
                }
            }

            if (!user) {
                this.$router.push({ name: 'LoginPage' });
            }

            let result = await axios.get('http://localhost:3000/restaurant');
            this.restaurant = result.data;
        }
    },
    async mounted() {

        this.loadData()

    },

}
</script>
<style scoped>
h3{
    margin-top: 10px;
}
table {
    margin: 10px auto;
    border: 1px solid #ccc;
    background-color: white;

}

td,
th {
    width: 160px;
    height: 40px;
    border: 1px solid #ccc;



}
.deleteBtn{
    width: 80px;
    height: 30px;
    background: red;
    color: #fff;
    border: none;
    border-radius: 5px;
}
.deleteBtn:hover{
    background-color: #851414;
    cursor: pointer;
}
.editBtn a{
    width: 80px;
    height: 30px;
    background: #108616;
    color: #fff;
    border: none;
    display: block;
    margin: 0 auto;
    border-radius: 5px;
    text-decoration: none;
    line-height: 30px;
}
.editBtn a:hover{
    background: #0f6413;
}
</style>