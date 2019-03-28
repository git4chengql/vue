<template>
  <div id="addC" class="container">
     <h3 class="page-header">添加用户</h3>
     <form v-on:submit="addCustomer">
       <div class="well">
          <h4>用户信息</h4>
          <div class="form-group">
    			<label>姓名</label>
    			<input type="text" class="form-control" placeholder="name" v-model="customer.name">
    		</div>
    		<div class="form-group">
    			<label>年龄</label>
    			<input type="text" class="form-control" placeholder="age" v-model="customer.age">
    		</div>
    		<div class="form-group">
    			<label>邮箱</label>
    			<input type="text" class="form-control" placeholder="email" v-model="customer.email">
    		</div>
        <div class="form-group">
    			<label>公司</label>
    			<input type="text" class="form-control" placeholder="公司" v-model="customer.companyId">
    		</div>
    		<button type="submit" class="btn btn-primary">添加</button>

       </div>
     </form>
  </div>
</template>

<script>


export default {
  name: 'addC',
  data(){
     return {
       customer:{}
     }
  },
  methods:{
    addCustomer(e){
      if(!this.customer.name || !this.customer.age || !this.customer.email){
        console.log("不能为空");
      }else{
        var newCustomer = {
            name:this.customer.name,
            age:this.customer.age,
            email:this.customer.email,
            companyId:this.customer.companyId
        }
        //请求服务器地址，提交数据
        this.$http.post("http://localhost:3000/users",newCustomer)
              .then(function(res){
                  this.$router.push({path:"/",query:{alert:"添加用户成功"}});
              })

      }
      e.preventDefault();
    }
  }
}
</script>

<style>

</style>
