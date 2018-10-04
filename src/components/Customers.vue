<template>
    <div class="customers container">
        <h1 class="page-header">Manage Customers</h1>
        <table class="table table-striped">
              <thead>
                <tr>
                  <th>#</th>
                  <th>First Name</th>
                  <th>Last Name</th>
                  <th>Email</th>
                  <th>Phone</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="customer in customers" :key="customer.id">
                  <td>{{customer.id}}</td>
                  <td>{{customer.first_name}}</td>
                  <td>{{customer.last_name}}</td>
                  <td>{{customer.email}}</td>
                  <td>{{customer.phone}}</td>
                </tr>
              </tbody>
            </table>
    </div>
</template>
<script>
export default {
  name: "customers",
  data() {
    return {
      customers: []
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
    this.fetchCustomers();
  },
  updated: function() {
    this.fetchCustomers();
  }
};
</script>

<style scoped>
</style>
