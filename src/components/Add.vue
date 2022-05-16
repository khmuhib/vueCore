<template>
    <Header></Header>
    <h1>Welcome To Add Restsurant</h1>
    <form action="" class="add">
        <input type="text" name="name" placeholder="Enter Name" v-model="restsurant.name">
        <input type="text" name="contact" placeholder="Enter Contact" v-model="restsurant.contact">
        <input type="text" name="address" placeholder="Enter Address" v-model="restsurant.address">
        <button @click="add" type="button">Add New Restsurant</button>
    </form>
</template>

<script>

import Header from './Header.vue'
import axios from 'axios'

export default {
    name: "Add-",
    data () {
        return {
            restsurant: {
                name: '',
                contact: '',
                address: ''

            }
        }
    },
    methods: {
        async add () {
            console.log(this.restsurant);
            const result = await axios.post("http://localhost:3000/restsurant", {
                name:this.restsurant.name,
                contact:this.restsurant.contact,
                address:this.restsurant.address
            });
            console.warn("result", result);
            if (result.status==201){
                this.$router.push({ name: "Home" });

            }

        }
    },
    mounted() {
        let user = localStorage.getItem("user-info");
        if (!user) {
            this.$router.push({ name: "SignUp" });
        }
    },
    components: { Header }
};
</script>
