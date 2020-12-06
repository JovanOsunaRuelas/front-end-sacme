<template>
     <div class="container table-responsive">
    <table toggleable="md" class="table table-dark table-hover table-bordered">
      <thead>
        <tr> 
          <th class="text-center">Id</th> 
          <th class="text-center">Fecha de Inicio</th> 
          <th class="text-center">Fecha Fin</th>
          <th class="text-center">Estacionamiento</th>
          <th class="text-center">Rol</th>
          
   
        </tr>
      </thead>
      <tbody v-for="lugarocupado in lugaresocupados" :key="lugarocupado.id">
          <td class="text-center">{{lugarocupado.id}}</td>
          <td class="text-center">{{lugarocupado.fecha_inicio}}</td>
          <td class="text-center">{{lugarocupado.fecha_fin}}</td>
          <td class="text-center">{{lugarocupado.estacionamiento}}</td>
          <td class="text-center">{{lugarocupado.roles}}</td>
          
        
      </tbody>
    </table>
    
  </div>
</template>

<script>
import axios from 'axios';

export default {
    name:'TablaInicio',
    data(){
      return{
        lugaresocupados: []
      }
    },

    mounted(){
      this.getlugarocupado()
    },
    methods:{
       getlugarocupado(){
        axios.get('http://localhost:8000/estacionamientos/lugares-ocupados/' )
            .then( data =>{
                console.log(data);
              this.lugaresocupados=data.data;
                
          
               
                    
                
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