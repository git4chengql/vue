<template>
  <div id="detail" class="container">
    <router-link to="/" class="btn btn-default">返回</router-link>
    <h3 class="page-header">
    	{{customer.name}}
      <span class="pull-right">
        <router-link v-bind:to="'/edit/'+customer.id" class="btn btn-success">编辑 {{customer.id}}</router-link>
        <button v-on:click="deleteCustomer(customer.id)" class="btn btn-danger">删除 {{customer.id}}</button>
      </span>
    </h3>
    <ul class="list-group">
       	<li class="list-group-item">
       		<span class="glyphicon glyphicon-asterisk">
       			{{customer.age}}
       		</span>
       	</li>
       	<li class="list-group-item">
       		<span class="glyphicon glyphicon-plus">
       			{{customer.email}}
       		</span>
       	</li>
       </ul>
  </div>
</template>

<script>


export default {
  name: 'detail',
  data(){
      return {
        customer:""
      }
  },
  methods:{
    fetchCustomers(id){
      this.$http.get("http://localhost:3000/users/"+id)
                  .then(function(res){
                      this.customer = res.body;
                  })
    },
    //deleteCustomer
    deleteCustomer(customerId){
      this.$http.delete("http://localhost:3000/users/"+customerId)
                  .then(function(res){
                      this.$router.push({path:'/',query:{alert:"删除成功"}});
                  })
    }
  },
  created(){
    this.fetchCustomers(this.$route.params.id);
  }
}
</script>

<style>

</style>
