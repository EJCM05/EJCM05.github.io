<template>
  <div class="app-wrapper">
    <TerminalWindows title="EJCM05">
      <NuxtPage />
    </TerminalWindows>
  </div>
</template>

<script setup>
import TerminalWindows from '@/components/TerminalWindows.vue';
</script>

<style>
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.13.1/font/bootstrap-icons.min.css");
/* Estilos globales para el body y el contenedor principal */
body {
  background-color: #111;
  /* Un fondo ligeramente más oscuro */
  margin: 0;
  min-width: 100vh;
}

.app-wrapper {
  min-width: 100vh;
}

/* Estilos para la barra de navegación dentro de la terminal */
.terminal-nav {
  display: flex;
  gap: 20px;
  justify-content: flex-end;
  /* A la derecha como en la imagen de tu primer ejemplo */
  margin-bottom: 30px;
  padding-bottom: 15px;
  border-bottom: 1px dashed #0F0;
  /* Un separador sutil verde */
  text-transform: uppercase;
  font-size: 0.8em;
}

.terminal-nav .nav-item {
  color: #0F0;
  /* Texto verde */
  text-decoration: none;
  font-weight: bold;
  transition: color 0.2s;
  padding: 2px 5px;
  /* Pequeño padding para hacerlos más clickeables */
  border: 1px dashed transparent;
  /* Borde sutil para hover */
}

.terminal-nav .nav-item:hover {
  color: #00FFFF;
  /* Un verde azulado al pasar el mouse */
  border-color: #00FFFF;
  /* Borde que aparece al pasar el mouse */
}

.help-output .cli-button,
.credits-output .cli-button {
  margin-top: 10px;
}

.cli-button {
  background-color: transparent;
  color: #FFF;
  border-radius: 4px;
  padding: 8px 15px;
  text-decoration: none;
  display: inline-block;
  font-weight: bold;
  border: 1px solid #1b8012;
  cursor: pointer;
  transition: background-color 0.2s, color 0.2s;
}

.cli-button:hover {
  background-color: #1b8012;
  color: black;
}

.start-button {
  display: block;
  margin: 2rem auto;
  width: 100% !important;
  background-color: transparent;
  border: 1px dashed #0F0;
  color: #0F0;
  font-weight: bold;
  text-transform: uppercase;
  cursor: pointer;
  padding: 2px 0;
}

.start-button:hover {
  background-color: #0F0;
  color: white;
}
</style>