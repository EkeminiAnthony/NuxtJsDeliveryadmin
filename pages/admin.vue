<template>
    <div>
        <div class="one">
            <h1>Orders</h1>
            <div class="table-responsive">
                <table class="table table-striped">
                    <thead>
                        <tr>
                        <th scope="col">First Name</th>
                        <th scope="col">Last Name</th>
                        <th scope="col">Email</th>
                        <th scope="col">Phone Number</th>
                        <th scope="col">Pickup Address</th>
                        <th scope="col">Dropoff Address</th>
                        <th scope="col">Freight Type</th>
                        <th scope="col">Order Description</th>
                        <th scope="col">Pickup Date</th>
                        <th scope="col">Pickup Time</th>
                        <th scope="col">Delete</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(tran,id) in orders" :key="id">
                        
                        <td>{{tran.firstname}}</td>
                        <td>{{tran.lastname}}</td>
                        <td>{{tran.email}}</td>
                        <td>{{tran.phonenumber}}</td>
                        <td>{{tran.pickup}}</td>
                        <td>{{tran.dropoff}}</td>
                        <td>{{tran.type}}</td>
                        <td>{{tran.description}}</td>
                        
                        <td>{{tran.date}}</td>
                        <td>{{tran.time}}</td>
                        <td><font-awesome-icon :icon="['fas', 'trash-alt']" @click.prevent="deletePost(id)" /></td>
                        </tr>
                        
                        
                    </tbody>
                </table>
            </div>
        </div>
        
    </div>
</template>


<script>
import 'element-ui/lib/theme-chalk/index.css';
import { FortAwesome } from '@fortawesome/free-brands-svg-icons'
export default {
    components:{
FortAwesome
    },
    data(){
        return{
           orders:{

           }
        }
    },
    mounted(){
        this.deliver()
    },
    methods : {
        deletePost(id){
            if (window.confirm("Do you really want to delete?")) {
               this.$axios.delete(`https://nuxtjs-delivery-app-default-rtdb.firebaseio.com/freedelivery/${id}.json`).then((res)=>{
            this.$message({
            message: "Deleted!!!",
            type: "success",
            });
           
          console.log(res)
         this.deliver()
          
        })
                .catch((error) => {
                    console.error(error);
                })
              }
            
        },
 
        async deliver() {
      try {
        this.$axios.get('https://nuxtjs-delivery-app-default-rtdb.firebaseio.com/freedelivery.json',this.deliveryorder)
        .then((res)=>{
            this.orders =res.data
           
          console.log(this.orders)
         
          
        })
      } catch (err) {
           this.$message({
            message: "There was a problem getting your orders. Please check and try again.",
            type: "warning",
            });
        console.log(err)
      }
    },
        
    }
}
</script>

<style scoped>
    .one{
        margin-top: 9rem;
        margin-left: 5%;
        margin-right: 5%;
    }
</style>