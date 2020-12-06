<template>
    <div class="Inicio">
        <NarBar/>
        <br>
        <h2 class="text-center">lugares ocupados</h2>
        <br>
       
        <br>
        <b-container>
            <TablaInicio/>
        </b-container>
        <Piepagina/>
    </div>
</template>

<script>
import NarBar from '@/components/NarBar.vue'
import Piepagina from '@/components/Piepagina.vue'
import TablaInicio from '@/components/TablaInicio.vue'

export default {
    name: 'inicio',
    
    components: { 
      NarBar,
      TablaInicio,
     Piepagina  
  }
}
</script>

<style scoped>

</style>