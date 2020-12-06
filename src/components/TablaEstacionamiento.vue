<template>
    <div class="container table-responsive">
    <table toggleable="md" class="table table-dark table-hover table-bordered">
      <thead>
        <tr> 
          <th class="text-center">Id</th> 
          <th class="text-center">Nombre</th> 
          <th class="text-center">Rol </th>
          <th class="text-center">Accion</th>
        </tr>
      </thead>
      <tbody v-for="estacionamiento in estacionamientos" :key="estacionamiento.id">
          <td class="text-center">{{estacionamiento.id}}</td>
          <td class="text-center">{{estacionamiento.nombre}}</td>
          <td class="text-center">{{estacionamiento.roles}}</td>
          <td class="text-center">
           <b-button  @click="buscarestacionamiento(estacionamiento.id)" variant="primary badge-pill" ><b-icon icon="pencil-square"></b-icon> Editar</b-button>

           
            <b-button variant="danger  badge-pill" style="width:70p;" @click="eliminar(estacionamiento.id)"><b-icon icon="person-x-fill"></b-icon> Eliminar</b-button>
          </td>
        
      </tbody>
    </table>
     <b-modal @ok="editor" id="edit" v-model="modalShow"  class="text-center">Editar Estacionamiento
              <b-container>
              <b-form-input v-model="nombre"  placeholder="Nombre"></b-form-input>
              <br>
              <b-form-select value-field="id" text-field="nombre" v-model="rol" :options="roles">rol</b-form-select>
              </b-container>
            </b-modal>
  </div>
</template>


<script>
import axios from 'axios'; 
export default {
    name:'TablaEstacionamiento',
    data() {
      return {
        modalShow: false,
        id: null,
        nombre: "",
        rol: null
        
       
      }
    },
    props:{
      estacionamientos:Array,
      roles:Array
    },
   
    methods:{
     
       eliminar(id){
     axios.delete(`http://localhost:8000/estacionamientos/estacionamientos/${id}` )
            .then( data =>{
                console.log(data);
            this.$emit("refrescartabla")
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
  },
  buscarestacionamiento(id){
      this.$bvModal.show("edit")

       axios.get(`http://localhost:8000/estacionamientos/estacionamientos/${id}` )
            .then( data =>{
                console.log(data);
            this.nombre=data.data.nombre
            this.id=data.data.id
            this.rol=data.data.roles
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
  },
  editor(){
    console.log(this.id)
    console.log(this.nombre)
    console.log(this.rol)
       axios.put(`http://localhost:8000/estacionamientos/estacionamientos/${this.id}/`,{ "nombre":this.nombre, "roles":parseInt(this.rol) } )
            .then( data =>{
                console.log(data);
              this.$emit("refrescartabla")
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
  }
  }
 
}
</script>