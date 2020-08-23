<template>
<div class="UpdateStatus">
<h1> {{msg}} </h1>
<form class="container">
   <div >
   <table id="sts">
   <thead>
   <tr>
            <th> Order Id</th>
             <th> Recipient Name </th>
             <th> Ordered Date </th>
             <th> Gift Card Value (Rs) </th>
             <th> Commission Amount (5%) </th> 
             <th> Amount Payable </th>
             <th> Update Delivery Status </th>
             
   </tr>
   </thead>
   <tbody v-for="sts in neworder" :key="sts.id">
   <tr>
        <td> {{sts.id}} </td>
          <td> {{sts.recFN}} {{sts.recLN}} </td>
            <td> {{sts.date}} </td>
              <td> INR {{sts.gcv}} </td>
                <td> INR {{sts.comAmt}} </td>
                <td> INR {{ sts.amtPay}} </td>
                <td>  <button type="button" @click="updateSts"> STS </button> </td>
               
              
   </tr>
   </tbody>
   
   </table>
   
      <button type="button" v-on:click="previous()"> Previous </button>  
<br>
        </div>
        
        </form>


</div>
</template>
<script>

export default {
    name:'updatestatus',
    data: function(){
       return{
           msg:'Bloom Gift Cards - Update Status Here',
           neworder:[],
           status:"Delivered"
       }
    },
    methods:{
        GetUpdateSts: function(){
            this.$http.get('http://localhost:3000/neworder')
            .then(res=> {
                console.log(res.data)
                this.neworder = res.data
            }, err=> {
                console.log(err)
            })
        },
         previous:function(){
          this.$router.push({path:'/adminprofile'})
          console.log("previous page")
        },
        updateSts:function(){
            // if(this.neworder[0].id === 1){
            //   this.neworder.sts == this.status
            //   console.log("del")
            // }
          
          if(this.neworder[0].id == 1){
             this.neworder.sts ="Delivered"
             this.neworder.push("Status Updated")
          return this.neworder.sts
          }
          return true
          
        }
    },
    
    created:function(){
    this.GetUpdateSts()
 //   console.log("get")
  //this.updateSts()
  // console.log("put")
  }
}
</script>
<style scoped>
#sts {

  border-collapse: collapse;
  width: 100%;
}

#sts td, #sts th {
  border: 1px solid #ddd;
  padding: 8px;
}

#sts tr:nth-child(even){background-color: #f2f2f2;}

#sts tr:hover {background-color: #ddd;}

#sts th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: center;
  background-color: #666699;
  color: white;
}
.container {
  padding: 16px;
  
}
button {
  background-color:rgb(90, 176, 216);
  color: white;
  padding: 10px;
  margin: 5px 0 22px 0;
  border: none;
  cursor: pointer;
  width: 18%;
  opacity: 0.9;
  
}
button:hover {
  opacity:1;
}
</style>