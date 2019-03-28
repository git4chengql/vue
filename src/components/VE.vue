<template>
  <div id="grid" class="container">
    <input type="text" class="form-control" placeholder="搜索" v-model="filterInput">
    <br>
    <DataGrid :data="filterBy(data,filterInput)"  :pagination=pagination style="height:250px">
            <GridColumn field="id" title="ID" align="center" idField></GridColumn>
            <GridColumn field="name" title="姓名" align="center"></GridColumn>
            <GridColumn field="age" title="年龄" align="center"></GridColumn>
            <GridColumn field="email" title="邮箱" align="center"></GridColumn>
            <GridColumn field="companyId" title="公司" width="30%"></GridColumn>
    </DataGrid>
  </div>
</template>

<script>


export default {
  name: 'grid',
  data(){
    return{
      filterInput:"",
      pagination:true,
      data:[],
      total:10,
      pageNumber:2,
      pagePosition:'left'
    }
  },
  methods:{
    initGrid(){
      this.$http.get("http://dept-8001.com:3000/users")
                  .then(function(res){
                      this.data = res.body;
                  })
    },
    filterBy(customers,skey){
      return customers.filter(function(customer){
           return customer.name.match(skey)||customer.age.match(skey)||customer.email.match(skey);
      })
    }
  },

  created(){
    this.initGrid();
  }
}
</script>

<style>

</style>
