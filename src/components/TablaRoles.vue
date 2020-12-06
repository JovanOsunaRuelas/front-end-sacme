<template>
    <div class="container table-responsive">
    <table toggleable="md" class="table table-dark table-hover table-bordered">
      <thead>
        <tr> 
          <th class="text-center">Id</th> 
          <th class="text-center">Nombre</th> 
          <th class="text-center">Descripcion</th>
          <th class="text-center">Accion</th>
        </tr>
      </thead>
      <tbody v-for="rol in roles" :key="rol.id">
          <td class="text-center">{{rol.id}}</td>
          <td class="text-center">{{rol.nombre}}</td>
          <td class="text-center">{{rol.descripcion}}</td>
          
          <td class="text-center">
           <b-button @click="geteditar(rol.id)" variant="primary badge-pill" ><b-icon icon="pencil-square"></b-icon> Editar</b-button>

            
            <b-button @click="roleliminar(rol.id)" variant="danger  badge-pill" style="width:70p;"><b-icon icon="person-x-fill"></b-icon> Eliminar</b-button>
          </td>
        
      </tbody>
    </table>
    <b-modal @ok="editador(id)" id="edito" v-model="modalShow"  class="text-center">Editar Rol
              <b-container>
                 <b-form-input v-model="id" hidden="" placeholder=""></b-form-input>
                <br>
              <b-form-input v-model="nombre"  placeholder="Nombre"></b-form-input>
              <br>
               <b-input v-model="descripcion" class="form-control" placeholder="Descripcion"/>
              
              </b-container>
            </b-modal>
  </div>
</template>


<script>
import axios from 'axios';

export default {
    name:'TablaRoles',
    data() {
      return {
        modalShow: false,
        id: null,
        nombre: "",
        descripcion: "",
        
      }
    },
    props:{
      roles: Array
    },
     methods:{
    
   roleliminar(id){
      axios.delete(`http://localhost:8000/estacionamientos/roles/${id}` )
            .then( data =>{
                console.log(data);
           this.$emit("refresca")
               
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
   },
   geteditar(id){
     this.$bvModal.show("edito")
     axios.get(`http://localhost:8000/estacionamientos/roles/${id}` )
            .then( data =>{
                console.log(data);
            this.nombre=data.data.nombre;
            this.descripcion=data.data.descripcion;
            this.id=data.data.id;   
                    
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
   },
   editador(id){
     console.log(this.id)
     console.log(this.nombre)
     console.log(this.descripcion)
      axios.put(`http://localhost:8000/estacionamientos/roles/${id}/`,  { "nombre":this.nombre, "descripcion":this.descripcion} )
            .then( data =>{
                console.log(data);
                this.$emit("refresca")
                
            } )
            .catch(e =>{
                
                
                    console.log(e);
            })
   }
  }
}
</script>