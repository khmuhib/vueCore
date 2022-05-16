<template>
  <Header></Header>
  <h1>
    Hello !!! <span style="color: red">{{ name }}</span
    >This is Home page.
  </h1>
  <table border="1">
    <tr>
      <td>Id</td>
      <td>Restsurant Name</td>
      <td>Restsurant Contact</td>
      <td>Restsurant Address</td>
      <td colspan="2">Action</td>
    </tr>
    <tr v-for="item in restsurant" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.contact }}</td>
      <td>{{ item.address }}</td>
      <td>
        <router-link :to="'/update/' + item.id">Update</router-link>
        <button v-on:click="deleteRes(item.id)" type="button">Delete</button>
      </td>
    </tr>
  </table>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";

export default {
  name: "Home-",
  data() {
    return {
      name: "",
      restsurant: [],
    };
  },

  components: {
    Header,
  },

  methods: {
    async deleteRes(id) {
      let result = await axios.delete("http://localhost:3000/restsurant/"+id);
      console.warn(result)
      if(result.status == 200) {
          this.loadData()
      }
    },
    async loadData () {
        let user = localStorage.getItem("user-info");
        this.name = JSON.parse(user).name;
        if (!user) {
        this.$router.push({ name: "SignUp" });
        }

        let result = await axios.get("http://localhost:3000/restsurant");
        console.warn(result);
        this.restsurant = result.data;

    },
  },

  async mounted() {
      this.loadData();
  },
};
</script>
