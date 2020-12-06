<template>
    <div class="usuarios">
    <NarBar/>
    <br>
     <div class="text-center">
      <h2> Usuarios</h2>
    </div>
    <br>
    <b-container>
      <b-row >
        <b-col>
          <b-col class="text-right">
          <div>
            <b-button @click="modalShow = !modalShow" variant="outline-primary" ><b-icon icon="plus-square"></b-icon>  Agregar Usuario</b-button>

            <b-modal @ok="guarda" v-model="modalShow">Ingrese Usuario Nuevo
                <b-container>
                    <br>
                  <b-form-input v-model="email" placeholder="Correo Electronico"></b-form-input>
                    <br>
                  <b-form-input v-model="usuario" placeholder="Usuario"></b-form-input>
                    <br>
                  <b-form-input v-model="nombre" placeholder="Nombre"></b-form-input>
                    <br>
                  <b-form-input v-model="priapellido" placeholder="Primer Apellido"></b-form-input>
                    <br>
                  <b-form-input v-model="seapellido" placeholder="Segundo Apellido"></b-form-input>
              
  
                </b-container>

            </b-modal>
            

          </div>
        </b-col>
        </b-col>
      </b-row>
    </b-container>
    <br>
    <br>
    <b-container>
      <TablaUsuarios :usuarios="usuarios" @refresco="getusuarios"/>
    </b-container>
    <br>
    <Piepagina/>
    
  </div>
</template>

<script>

import NarBar from '@/components/NarBar.vue'
import Piepagina from '@/components/Piepagina.vue'
import TablaUsuarios from '@/components/TablaUsuarios.vue'
import axios from 'axios';

export default {
    name: 'Usuarios',
  components: { 
      NarBar,
      TablaUsuarios,
      Piepagina 
  },
    data() {
      return {
        modalShow: false,
        email: "",
        usuario: "",
        nombre: "",
        priapellido: "",
        seapellido: "",
        usuarios: []
      }
    },
    mounted(){
      this.obtusuarios()
      this.getusuarios()
    },
    methods:{
      obtusuarios(){
        axios.get('http://localhost:8000/usuarios/usuarios/' )
            .then( data =>{
                console.log(data);
               this.getusuarios();
          
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
   },
   guarda(){
     axios.post('http://localhost:8000/usuarios/usuarios/', {"email":this.email, "username":this.usuario, "first_name":this.nombre, "last_name":this.priapellido, "second_last_name":this.seapellido } )
            .then( data =>{
                console.log(data);
               this.getusuarios();
          
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
   },
   getusuarios(){
        axios.get('http://localhost:8000/usuarios/usuarios/' )
            .then( data =>{
                console.log(data);
                this.usuarios=data.data;
          
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
   },
  
    }
}

</script>