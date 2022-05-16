<template>
    <div class="nav">
            <router-link to="/" href="#">Home</router-link>
            <router-link to="/add" href="#">Add Restaurant</router-link>
            <!-- <router-link to="/update" href="#">Update Restaurant</router-link> -->
            <a @click="logout" href="#">Logout</a>
    </div>
</template>

<script>
export default {
    name: 'Header-',

    methods: {
        logout () {
            localStorage.clear();
            this.$router.push({name:'Login'})
        }
    }
}
</script>

<style scoped>
.nav {
    background: #333;
    overflow: hidden;
}

.nav a {
    float: left;
    color: #fff;
    padding: 14px 16px;
    text-align: center;
    font-size: 17px;
    text-decoration: none;
    margin-left: 5px;
}

.nav a:hover {
    background-color: gray;
    color: #000;
}
</style>