<template>
       <div id="narbar">
  <b-navbar toggleable="md" type="dark" variant="dark">
    <b-container>

      <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>
   <b-navbar-brand href="#" >SACME</b-navbar-brand>

    <b-collapse is-nav id="nav_collapse">
      <b-navbar-nav>
     <b-nav-item :to="{name: 'Inicio'}" exact>Inicio</b-nav-item>   
     <b-nav-item :to="{name: 'Usuarios'}">Usuarios</b-nav-item> 
     <b-nav-item :to="{name: 'Roles'}">Roles</b-nav-item> 
     <b-nav-item :to="{name: 'Estacionamiento'}">Estacionamientos</b-nav-item>
    </b-navbar-nav> 
     <b-navbar-nav class="ml-auto">
       <b-nav-item class="por" :to="{name: 'Home'}"><b-icon icon="box-arrow-right"></b-icon> Cerrar sesion</b-nav-item>
     </b-navbar-nav>
      
    </b-collapse>  

    </b-container>
  </b-navbar>
</div>
</template>

<script>
export default {
  name: 'NarBar'
}
</script>

<style scoped>
por{
  text-align: right;
}
</style>

  