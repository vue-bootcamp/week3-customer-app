<template>
  <div id="app">
    <h1>Customer</h1>
    <hr>
    <input v-model="formData.firstName" type="text" class="form-control" placeholder="First name...">
    <input v-model="formData.lastName" type="text" class="form-control" placeholder="Last name...">
    <input v-model="formData.email" type="text" class="form-control" placeholder="Email...">
    <button @click="addCustomer" :class="btnDisable" class="btn btn-primary" style="width: 100%; margin-bottom: 25px;">ADD CUSTOMER</button>
    <customer-list
      v-if="customers.length > 0"
      :items="customers"
    />
  </div>
</template>

<script>
import CustomerList from "./components/CustomerList";

export default {
  name: 'App',
  components: {
    customerList : CustomerList
  },
  data() {
    return {
      formData: {
        firstName: "",
        lastName: "",
        email: "",
      },
      customers: [],
    }
  },
  methods: {
    clearForm() {
      this.formData = {
        firstName: "",
        lastName: "",
        email: "",
      }
    },
    addCustomer() {
      this.customers.push({
        id: this.customers.length + 1,
        ...this.formData
      });
      this.clearForm();
    }
  },
  computed: {
    btnDisable() {
      return {
        "disabled" : this.formData.firstName === "" || this.formData.lastName === "" || this.formData.email === ""
      };
    },
  }
}
</script>

<style>
#app {
  width: 85%;
  margin: 50px auto;
}
input {
  margin: 15px 0px;
}
</style>
