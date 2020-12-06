<template>
<div class="main" >
    <div class="modal-dialog text-center">
         <div class="col-sm-10 main-section">
             <div class="modal-content ">
                 <div class="col-24">
                     <img class="col-12" src="../assets/sacme-logo.jpg">
                 </div>
                 <br>
    <form class="col-12" v-on:submit.prevent="login">
     <div class="form-group">   
        <b-input-group size="lg">
            <b-input-group-prepend is-text>
                 <b-icon icon="envelope"></b-icon>
            </b-input-group-prepend>
            <b-form-input v-model="email" type="email" placeholder="Correo electronico"></b-form-input>
            </b-input-group>
                            
                    
     </div>
        <div class="form-group">   
            <b-input-group size="lg">
                <b-input-group-prepend is-text>
                    <b-icon icon="file-lock"></b-icon>
                </b-input-group-prepend>
                <b-form-input v-model="password" type="password" placeholder="Contraseña"></b-form-input>
                </b-input-group>
    </div>
                 <br>
                    <b-button type="submit"><b-icon icon="person-fill"></b-icon>Iniciar sesion</b-button>
             </form>
             <b-alert show variant="danger" v-if="error" >{{error_msg}}</b-alert>
             <br>
             <div class="col-12 forgot">
                   <p class="mt-3">No Tienes Cuenta? <a href="registro">Registrarse!</a></p>
                </div>
                <br>
             </div>
         </div>
    </div>   

</div>   
</template>

<script>
// @ is an alias to /src
import axios from 'axios'; 

export default {
  name: 'Home',
  components: {

  },
  data: function(){
      return{
          email: "",
          password: "",
          error: false,
          error_msg: "",
      }
  },
  
methods:{
      login(){
          let json = {
              "email" : this.email,
              "password" : this.password
          };
            axios.post('http://localhost:8000/usuarios/login/', json)
            .then( data =>{
                console.log(data);
               
                    localStorage.token = data.data.access;
                    this.$router.push('inicio');
                
            } )
            .catch(e =>{
                
                this.error = true;
                    this.error_msg = e;
                    console.log(e.body);
            })
      }
  }
}
</script>

<style scoped>
template{
    margin: 0;
    padding: 0;
}
.main {
    background-image:  url(../assets/fondo-login.png);
    background-repeat: no-repeat;
    width: 100%;
    height: 100%;
    position: absolute;
    background-size: cover;
    
}
.main-section{
    
    margin-left: 110%;
    margin-top: 50%;
}




    
</style>
