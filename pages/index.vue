<template>
    <div class="container-fluid ">
        <div class="container margin_top">
            <div class="card shadow rounded" >
            <div class="card-body">
                <form @submit.prevent="login">
                    <h5 class="modal-title" id="exampleModalLabel">ADMIN LOG IN</h5>
                    <hr>
                    <div class="form-group">
                        
                            <label for="exampleInputEmail1">Email address</label>
                            <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter email" v-model="auth.email">
                            <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
                        </div>
                        <div class="form-group">
                            <label for="exampleInputPassword1">Password</label>
                            <input type="password" class="form-control" id="exampleInputPassword1" placeholder="Password" v-model="auth.password">
                            <small id="emailHelp" class="form-text text-muted click_pass">Forgot Password?Cick here</small>
                        </div>
                        <div class="form-group form-check">
                            <input type="checkbox" class="form-check-input" id="exampleCheck1">
                            <label class="form-check-label" for="exampleCheck1">Remember me</label>
                        </div>
                        
                        <!-- <button type="submit" class="btn btn-primary">LOG IN</button> -->
                         <button type="submit" class="btn btn-primary">
                            <span v-if="notloading">LOG IN</span>
                            <div v-else><loader/></div>
                        </button>
        </form>
            </div>
            </div>
        </div>
    </div>
</template>

<script>
import firebase from 'firebase'
import loader from '@/components/loader'

export default {
    components:{
        firebase, loader
    },
    data(){
        return{
          auth:{
            
            email:'',
            password:''
          },
          notloading : true
            
        }
    },
    created(){
         
      
        
    },
    methods: {
        
        login(){
            this.notloading = false;
            firebase.auth().signInWithEmailAndPassword(this.auth.email, this.auth.password)
                .then((userCredential) => {
                    this.$router.push('/admin');
                    // Signed in
                    var user = userCredential.user;
                    console.log(user)
                     this.notloading = true;
                    // ...
                })
                .catch((error) => {
                    var errorCode = error.code;
                    var errorMessage = error.message;
                    this.notloading = true;
                    console.log(errorCode)
                    console.log(errorMessage)
                });
        }
        
        

    }
    
}

</script>

<style scoped>
.card{
    width: 30%;
    margin-left: 25rem;
}
.margin_top{
    margin-top: 13rem !important;
}
.click_pass{
    cursor: pointer;
}
.btn-primary {
    color: white;
    border-color: #f15f22 !important;
    background-color:  #f15f22 !important;
    text-transform: capitalize;
}
@media only screen and (max-width: 600px) {
.card{
    width: 100%;
    margin-left: 0;
}
.margin_top{
    margin-top: 13rem !important;
}
.click_pass{
    cursor: pointer;
} 
}
@media only screen and (min-width: 700px)  and (max-width: 1200px) {
.card{
    width: 50%;
    margin-left: 10rem !important;
}
.margin_top{
    margin-top: 13rem !important;
}
.click_pass{
    cursor: pointer;
} 
} 


</style>