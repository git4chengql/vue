<template>
  <div id="customers" class="container">
    <Alert v-if="alert" v-bind:message="alert"></Alert>
    <h3 class="page-header">用户管理系统</h3>
    <input type="text" class="form-control" placeholder="搜索" v-model="filterInput">
    <br>
    <table class="table table-striped">
       <thead>
          <tr>
            <th>姓名</th>
            <th>年龄</th>
            <th>邮箱</th>
            <th></th>
          </tr>
       </thead>
       <tbody>
         <tr v-for="customer in filterBy(customers,filterInput)">
            <td>{{customer.name}}</td>
            <td>{{customer.age}}</td>
            <td>{{customer.email}}</td>
            <td><router-link class="btn btn-default" v-bind:to="'/user/'+customer.id">详情</router-link></td>
         </tr>
       </tbody>
    </table>
  </div>
</template>

<script>

import Alert from './Alert'
export default {
  name: 'customers',
  data(){
      return {
        customers:[],
        alert:"",
        filterInput:""
      }
  },
  methods:{
    fetchCustomers(){
      this.$http.get("http://dept-8001.com:3000/users")
                  .then(function(res){
                      this.customers = res.body;
                  })
    },
    filterBy(customers,skey){
      return customers.filter(function(customer){
           return customer.name.match(skey);
      })
    }
  },
  created(){
    if(this.$route.query.alert){
      this.alert = this.$route.query.alert;
    }
   this.fetchCustomers();
  },
  mounted(){
    this.fetchCustomers();
  },
  components:{
    Alert
  }
}
</script>

<style>

</style>
