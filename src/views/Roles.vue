<template>
    <div class="Roles">
        <NarBar/>
         <br>
     <div class="text-center">
      <h2> Roles</h2>
    </div>
    <br>
    <b-container>
      <b-row >
        <b-col>
          <b-col class="text-right">
          <div>
            <b-button @click="modalShow = !modalShow" variant="outline-primary" ><b-icon icon="plus-square"></b-icon>  Agregar </b-button>

            <b-modal @ok="guardar" v-model="modalShow">ingresar Rol
                <b-container>
                  <br>
              <b-form-input v-model="nombre" placeholder="Nombre"></b-form-input>
                <br>
              <b-form-input v-model="descripcion" placeholder="Descripcion"></b-form-input>
               
              
  
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
            <TablaRoles :roles="roles" @refresca="getrol" />
        </b-container>
        <Piepagina/>
    </div>
</template>

<script>
import NarBar from '@/components/NarBar.vue'
import Piepagina from '@/components/Piepagina.vue'
import TablaRoles from '@/components/TablaRoles.vue'
import axios from 'axios';

export default {
    name: 'roles',
    components: { 
      NarBar,
      TablaRoles,
      Piepagina 
  },
   data() {
      return {
        modalShow: false,
        nombre: "",
        descripcion: "",
        roles: []
        
      }
    },
    mounted(){
      this.getrole()
      this.getrol()
    },
    methods:{
      getrole(){
        axios.get('http://localhost:8000/estacionamientos/roles/' )
            .then( data =>{
                console.log(data);
           this.roles=data.data;
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
   },
   guardar(){
     axios.post('http://localhost:8000/estacionamientos/roles/', {"nombre":this.nombre, "descripcion":this.descripcion} )
            .then( data =>{
                console.log(data);
                this.getrol
               this.getrol();
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
   },
    getrol(){
     axios.get('http://localhost:8000/estacionamientos/roles/' )
            .then( data =>{
                console.log(data);
           this.roles=data.data;
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
   }
      }
    }

</script>

<style scoped>

</style>