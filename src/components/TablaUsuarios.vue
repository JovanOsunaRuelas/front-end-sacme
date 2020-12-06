<template>
    <div class="container table-responsive">
    <table toggleable="md" class="table table-dark table-hover table-bordered">
      <thead>
        <tr> 
            <th class="text-center">Id</th> 
            <th class="text-center">Correo</th> 
            <th class="text-center">Usuarios</th>
            <th class="text-center">Nombre</th>
            <th class="text-center">Primer Apelido</th>
            <th class="text-center">Segundo Apellido</th>
            <th class="text-center">Accion</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="usuario in usuarios" :key="usuario.id">
          <td class="text-center">{{usuario.id}}</td>
          <td class="text-center">{{usuario.email}}</td>
          <td class="text-center">{{usuario.username}}</td>
          <td class="text-center">{{usuario.first_name}}</td>
          <td class="text-center">{{usuario.last_name}}</td>
          <td class="text-center">{{usuario.second_last_name}}</td>
          <td class="text-center">

            <b-button @click="getbuscarusuarios(usuario.id)" variant="primary badge-pill"><b-icon icon="pencil-square"></b-icon> Editar</b-button>

         
            <b-button variant="danger  badge-pill" style="width:70p;" @click="usueliminar(usuario.id)"><b-icon icon="person-x-fill"></b-icon> Eliminar</b-button>
           
          </td>
        </tr>
      </tbody>
    </table>
       <b-modal @ok="editadorput(id)" id="editar" v-model="modalShow"  class="text-center">Editar Usuario
              <b-container>
                <b-form-input v-model="id" hidden="true" placeholder=""></b-form-input>
            <br>
                  <b-form-input v-model="emaill" placeholder="Correo Electronico"></b-form-input>
                    <br>
                  <b-form-input v-model="usuarioo" placeholder="Usuario"></b-form-input>
                    <br>
                  <b-form-input v-model="nombree" placeholder="Nombre"></b-form-input>
                    <br>
                  <b-form-input v-model="primerapellido" placeholder="Primer Apellido"></b-form-input>
                    <br>
                  <b-form-input v-model="segundoapellido" placeholder="Segundo Apellido"></b-form-input>
              </b-container>
            </b-modal>
  </div>
</template>


<script>
import axios from 'axios';
export default {
    name:'TablaUsuarios',
     data() {
      return {
        modalShow: false,
        emaill: "",
        usuarioo: "",
        nombree: "",
        primerapellido: "",
        segundoapellido: "",
        id: null

      }
    },
    props:{
      usuarios:Array
    },
    
    methods:{
   usueliminar(id){
      axios.delete(`http://localhost:8000/usuarios/usuarios/${id}`, {"email":this.email, "username":this.usuario, "first_name":this.nombre, "last_name":this.priapellido, "second_last_name":this.seapellido } )
            .then( data =>{
                console.log(data);
              this.$emit("refresco")
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
   },
    
    getbuscarusuarios(id){
      this.$bvModal.show("editar")
         axios.get(`http://localhost:8000/usuarios/usuarios/${id}`, )
            .then( data =>{
                console.log(data);
              this.emaill=data.data.email;
              this.usuarioo=data.data.username;
              this.nombree=data.data.first_name;
              this.primerapellido=data.data.last_name;
              this.segundoapellido=data.data.second_last_name;
              this.id=data.data.id;
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
    },
    editadorput(id){
      console.log(this.emaill)
      console.log(this.usuarioo)
      console.log(this.nombree)
      console.log(this.primerapellido)
      console.log(this.segundoapellido)
       axios.put(`http://localhost:8000/usuarios/usuarios/${id}/`, {"email":this.emaill, "username":this.usuarioo, "first_name":this.nombree, "last_name":this.primerapellido, "second_last_name":this.segundoapellido } )
            .then( data =>{
                console.log(data);
              this.$emit("refresco")
              
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
    }  
    }  
  }

</script>