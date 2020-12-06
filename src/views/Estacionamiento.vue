<template>
    <div class="Estacionamiento">
        <NarBar/>
        <br>

        <div class="text-center">
      <h2> Estacionamientos</h2>
    </div>
    <br>
    <b-container>
      <b-row >
        <b-col>
          <b-col class="text-right">
          <div>
            <b-button @click="modalShow = !modalShow" variant="outline-primary" ><b-icon icon="plus-square"></b-icon> Agregar Estacionamiento</b-button>

            <b-modal @ok="aceptar" v-model="modalShow">Ingresar Estacionamiento
                <b-container>
                  <br>
              <b-form-input v-model="nombre" placeholder="Nombre"></b-form-input>
              
                <br>
              <b-form-select value-field="id" text-field="nombre" v-model="rol" :options="roles">rol</b-form-select>
              
  
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
        <TablaEstacionamiento :estacionamientos="estacionamientos" @refrescartabla="getestacionamientos" :roles="roles"/>
        </b-container>
        <Piepagina/>
    </div>
</template>

<script>
import NarBar from '@/components/NarBar.vue'
import Piepagina from '@/components/Piepagina.vue'
import TablaEstacionamiento from '@/components/TablaEstacionamiento.vue'
import axios from 'axios';

export default {
    name: 'estacionamiento',
    components: { 
      NarBar,
      TablaEstacionamiento,
      Piepagina 
  },
   data() {
      return {
        modalShow: false,
        nombre: "",
        rol: null,
        roles: [],
        estacionamientos: []
      }
    },
    methods:{
      getroles(){
        axios.get('http://localhost:8000/estacionamientos/roles/' )
            .then( data =>{
                console.log(data);
                this.roles=data.data;
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
      },
      aceptar(){
          axios.post('http://localhost:8000/estacionamientos/estacionamientos/',{"nombre":this.nombre, "roles":this.rol} )
            .then( data =>{
                console.log(data);
                this.getestacionamientos();
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
      },
      getestacionamientos(){
         
            axios.get('http://localhost:8000/estacionamientos/estacionamientos/' )
            .then( data =>{
                console.log(data);
                this.estacionamientos=data.data;
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
      },
  
    },
    mounted(){
      this.getroles()
      this.getestacionamientos()
    }
}
</script>

<style scoped>

</style>