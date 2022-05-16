<template>
    <Header></Header>
    <h1>Welcome To Update Restsurant</h1>
    <form action="" class="update">
        <input type="text" name="name" placeholder="Enter Name" v-model="restsurant.name">
        <input type="text" name="contact" placeholder="Enter Contact" v-model="restsurant.contact">
        <input type="text" name="address" placeholder="Enter Address" v-model="restsurant.address">
        <button @click="update" type="button">Update Restsurant</button>
    </form>
</template>

<script>

import Header from './Header.vue'
import axios from 'axios'

export default {
    name: "Update-",
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
        async update () {
            const result = await axios.put("http://localhost:3000/restsurant/"+this.$route.params.id, {
                name:this.restsurant.name,
                contact:this.restsurant.contact,
                address:this.restsurant.address
            });
            console.warn("result", result);
            if (result.status==200){
                this.$router.push({ name: "Home" });

            }

        }
    },
    async mounted() {
        let user = localStorage.getItem("user-info");
        if (!user) {
            this.$router.push({ name: "SignUp" });
        }
        const result = await axios.get('http://localhost:3000/restsurant/'+this.$route.params.id);
        console.warn(result);
        this.restsurant = result.data;
    },
    components: { Header }
};
</script>
