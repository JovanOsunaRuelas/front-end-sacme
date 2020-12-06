<template>
<div class="main">
   <div class="modal-dialog text-center">
         <div class="col-sm-10 main-section">
             <div class="modal-content ">
                 <div class="col-24">
                     <img class="col-12" src="../assets/sacme-logo.jpg">
                 </div>
                 <br>
                 <h3>Registrate</h3>
                  <form class="col-12" @submit.prevent.stop="registropost">
                 <div class="form-group" v>
                      <b-form-input v-model="correo" type="email"  class="form-control" placeholder="Correo"></b-form-input>
                </div>
                 <div class="form-group">   
                    <b-form-input v-model="nombre" type="text" class="form-control" placeholder="Nombre"></b-form-input>
                 </div>
                 <div class="form-group">   
                    <b-form-input v-model="apellido" type="text"  class="form-control" placeholder="Apellido"></b-form-input>
                 </div>
                        <div class="form-group">   
                    <b-form-input v-model="usuario" type="text"  class="form-control" placeholder="Usuario"></b-form-input>
                 </div>
                  <div class="form-group">   
                    <b-form-input v-model="contraseña" type="password" name="contraseña" class="form-control" placeholder="Contraseña"></b-form-input>
                 </div>
                 <br>
                    <b-button  variant="success" type="submit"><b-icon icon="person-plus"></b-icon> Registrarse</b-button>
                    
             </form>
              <div class="col-12 forgot">
                   <p class="mt-3"> ya te registraste? <a href="/">Inicia sesion</a></p>
                </div>
             <br>
                <br>
             </div>
         </div>
    </div> 
</div>   
</template>

<script>
import axios from 'axios';

export default {
   data(){
      return{
         correo: "",
         nombre: "",
         apellido: "",
         usuario: "",
         contraseña: ""
      }
   },
   methods:{
    registropost(){
          axios.post('http://localhost:8000/usuarios/registro/',{"email":this.correo, "first_name":this.nombre, "last_name":this.apellido, "username":this.usuario, "password":this.contraseña} )
            .then( data =>{
                console.log(data);
              this.$router.push("/")
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
      }
   },
  
}

</script>

<style scoped>


    
</style>