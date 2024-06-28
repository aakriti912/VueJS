<template>
    <div>
    <img src="https://th.bing.com/th/id/OIP.g5AKW21APdv9ToQ-pwgo9AHaGK?rs=1&pid=ImgDetMain" alt="logo" class="logo"/>
  <h1>Sign Up</h1>
    <div  class="register">
        <input type="text" v-model="name" placeholder="Enter name"/>
        <input type="text" v-model="email"  placeholder="Enter mail"/>
        <input type="password" v-model="password"  placeholder="Enter password"/>
<button v-on:click="signUp"> Sign Up</button>
    </div>
</div>
</template>

<script>
import axios from 'axios';



export default {
name:'SignUp',
data()
{
    return{
        name:'',
        email:'',
        password:''
    }
},
methods:{
     async signUp(){
        console.log("signup",this.name, this.email, this.password)
        let result = await axios.post("http://localhost:3000/user",{
            email:this.email,
            name:this.name,
            password:this.password


        });
        console.log(result)
        if(result.status == 201){
          
            localStorage.setItem("user-info", JSON.stringify(result.data));
            this.$router.push({name:'HomePage'})
        }
        
    }
},
mounted(){
    let user = localStorage.getItem("user-info");
    if(user){
        this.$router.push({name:'HomePage'})
    }
}
}

</script>

<style>
.logo{
    width: 100px;
    height: 100px;
}
.register{
    display: grid;
    justify-content: center;
}
.register input{
    width: 300px;
    height: 40px;
    display: grid;
    margin-bottom: 30px;
    border: 1px solid black;
    justify-content: center;
}
.register button{
    width: 320px;
    background-color: orange;
    height: 40px;
    color:white;
    cursor: pointer;
}

</style>