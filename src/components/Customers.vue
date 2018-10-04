<template>
    <div class="customers container">
        <Alert v-if="alert" v-bind:message="alert" />
        <h1 class="page-header">Manage Customers</h1>
        <table class="table table-striped">
              <thead>
                <tr>
                  <th>#</th>
                  <th>First Name</th>
                  <th>Last Name</th>
                  <th>Email</th>
                  <th>Phone</th>
                  <th>Action</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="customer in customers" :key="customer.id">
                  <td>{{customer.id}}</td>
                  <td>{{customer.first_name}}</td>
                  <td>{{customer.last_name}}</td>
                  <td>{{customer.email}}</td>
                  <td>{{customer.phone}}</td>
                  <td><router-link class="btn btn-default" v-bind:to="'/customer/' + customer.id">View</router-link></td>
                </tr>
              </tbody>
            </table>
    </div>
</template>
<script>
import Alert from "./Alert";

export default {
  name: "customers",
  data() {
    return {
      customers: [],
      alert: ""
    };
  },
  methods: {
    fetchCustomers() {
      this.$http
        .get("http://18.224.92.68/index.php/api/customers")
        .then(function(response) {
          this.customers = response.body;
          //console.log(response.body);
        });
    }
  },
  created: function() {
    if (this.$route.query.alert) {
      this.alert = this.$route.query.alert;
    }
    this.fetchCustomers();
  },
  updated: function() {
    this.fetchCustomers();
  },
  components: {
    Alert
  }
};
</script>

<style scoped>
</style>
