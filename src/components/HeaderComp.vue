<template lang="">
    <div class="nav">
        <router-link to="/">Home</router-link>
        <router-link to="add">Add Restaurant</router-link>
        <a v-on:click="logout" href="">Logout</a>
    </div>
</template>
<script>
export default {
    name:'HeaderComp',
    methods:{
        logout(){
            
            localStorage.clear();
            this.$router.push({name:'LoginPage'})
        }
    }
}
</script>
<style scoped>

    .nav{
        background:#f0efee;
        overflow: hidden;
        border-bottom: 1px solid #dfdfdc;

    }
    .nav a{
        float: left;
        color:rgb(78, 77, 77);
        padding: 14px 16px;
        text-align: center;
        text-decoration: none;
        margin-right: 5px;
        font-weight: 500;
    }
    .nav a:hover{
        background-color: #dfdedc;
    }
</style>