<template>
  <div>
    <div v-if="!isReady && !isLoading" class="loading-screen">

      <pre class="ascii-art" :class="{ 'glitch-effect': !isLoading }">
       _____  _               _____ 
      |  ___ | |             /  __ \
      | |__  | |__   ___ _ __| /  \/
      |  __| | '_ \ / _ \ '__| |   <
      | |___ | |_) |  __/ |  | \__/\
      |____/ |_.__/ \___|_|   \____/         
      </pre>
      <div class="container-column">
        <div class="info-box">
          <p><span class="green-text">========= </span> Portafolio <span class="green-text">=========</span></p>
          <p><span class="green-text">Creado Por:</span> Eber Colmenares </p>
          <p><span class="green-text">Version:</span> 1.0.0 </p>
          <p><span class="green-text">GitHub:</span> @EJCM05 </p>
          <p><span class="green-text">==============================</span></p>
        </div>
      </div>
    </div>
    <button @click="startLoading" v-if="!isReady && !isLoading" class="start-button cli-button w-100">START</button>
    <div v-if="isLoading" class="loading-bar-container">
      <div class="progress-bar-label">
        <p>Initializing system... [{{ loadingProgress }}%]</p>
      </div>
      <div class="progress-bar">
        <div class="progress-bar-fill" :style="{ width: loadingProgress + '%' }"></div>
      </div>
    </div>

    <div v-if="isReady" class="main-menu-content">
      <p class="select-option">Selecciona una opcion :</p>
      <ul class="cli-menu">
        <li>[01] <NuxtLink to="/about" class="cli-option">Sobre mi (sudo)</NuxtLink>
        </li>
        <li>[02] <NuxtLink to="/projects" class="cli-option">Ver Proyectos (ls -la)</NuxtLink>
        </li>
        <li>[03] <a href="https://github.com/EJCM05" target="_blank" rel="noopener noreferrer" class="cli-option">GITHUB
            REPO (GIT CLONE)</a></li>
        <li>[04] <NuxtLink to="/contact" class="cli-option">Contacto (MAIL -S)</NuxtLink>
        </li>
        <li>[05] <span @click="showHelp" class="cli-option clickable">Ayuda (MAN)</span></li>
        <li>[06] <span @click="showCredits" class="cli-option clickable">Créditos (CAT /ETC/CREDITS)</span></li>
      </ul>

      <div v-if="showingHelp" class="help-output">
        <p>Opciones disponibles:</p>
        <p>- Sobre mi: Información especifica.</p>
        <p>- Ver Proyectos: Proyectos desarrollados.</p>
        <p>- Repositorio: Enlace al perfil de GitHub.</p>
        <p>- Contacto: Metodos de contacto.</p>
        <button @click="hideHelp" class="cli-button">CLOSE</button>
      </div>
      <div v-if="showingCredits" class="credits-output">
        <p>Créditos:</p>
        <p>Desarrollado con Nuxt 3, Vue 3, Vite.</p>
        <p>Inspirado en interfaces de terminal antiguas.</p>
        <p>Creador: Eber Josue Colmenares Mendoza | Full stack Developer (Especialista en backend)</p>
        <button @click="hideCredits" class="cli-button">CLOSE</button>
      </div>
    </div>

    <p v-if="isReady" class="cli-prompt">
      $ root:@EberC:<span class="cursor">_</span>
    </p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const isReady = ref(false);
const isLoading = ref(false);
const loadingProgress = ref(0);

const showingHelp = ref(false);
const showingCredits = ref(false);

const startLoading = () => {
  isLoading.value = true;
  let interval = setInterval(() => {
    if (loadingProgress.value < 100) {
      loadingProgress.value += 10;
    } else {
      clearInterval(interval);
      isLoading.value = false;
      isReady.value = true;
    }
  }, 100);
};

const showHelp = () => {
  showingHelp.value = true;
  showingCredits.value = false;
};

const hideHelp = () => {
  showingHelp.value = false;
};

const showCredits = () => {
  showingCredits.value = true;
  showingHelp.value = false;
};

const hideCredits = () => {
  showingCredits.value = false;
};
</script>

<style scoped>
/* AÑADE ESTOS ESTILOS AL FINAL DE TU SECCIÓN <style scoped> */

/* Estilos de la pantalla inicial con grid */
.loading-screen {
  width: 100%;
  display: grid;
  grid-template-columns: auto auto;
  /* <--- ¡Cambiamos '1fr' a 'auto'! */
  justify-content: center;
  /* <--- Agregamos esto para centrar los elementos */
  align-items: center;
  gap: 20px;
  padding: 2rem 0;
  border: 1px dashed #0F0;
}

/* El ASCII art ahora es parte de la primera columna del grid */
.ascii-art {
  grid-column: 1;
  text-align: start;
  font-size: 1.2rem;
}

.container-column {
  grid-column: 2;
}

/* --- GLITCH EFFECT ANIMATION --- */
.glitch-effect {
  animation: glitch 1.5s infinite alternate;
  position: relative;
}

@keyframes glitch {
  0% {
    opacity: 1;
    text-shadow: none;
  }

  20% {
    opacity: 0.9;
    text-shadow: 2px -2px 0 rgba(255, 0, 0, 0.7), -2px 2px 0 rgba(255, 0, 0, 0.7);
  }

  40% {
    opacity: 1;
    text-shadow: none;
  }

  60% {
    opacity: 0.8;
    text-shadow: -3px -1px 0 rgba(255, 255, 255, 0.7), 3px 1px 0 rgba(255, 0, 0, 0.7);
  }

  80% {
    opacity: 0.95;
    text-shadow: 1px 1px 0 rgba(0, 255, 0, 0.7), -1px -1px 0 rgba(255, 0, 0, 0.7);
  }

  100% {
    opacity: 1;
    text-shadow: none;
  }
}

/* Fin de la animación GLITCH */


/* Tus estilos existentes (asegúrate de que no haya duplicados o conflictos) */
.ascii-art {
  color: #0F0;
  font-size: 1.2rem;
  margin-bottom: 20px;
  white-space: pre-wrap;
  width: 100%;
}

.info-box {
  text-align: center;
  color: #FFF;
}

.info-box p {
  margin: 25px 0;
}

.info-box p .green-text {
  color: #0F0;
}

.main-menu-content {
  min-width: 100vh;
}

/* Resto de tus estilos */
.loading-bar-container {
  width: 90%;
  max-width: 600px;
  margin: 50px auto;
  color: #0F0;
  text-align: center;
}

.progress-bar-label {
  font-family: 'Consolas', monospace;
  margin-bottom: 10px;
}

.progress-bar {
  width: 100%;
  height: 20px;
  border: 1px solid #0F0;
  border-radius: 4px;
  overflow: hidden;
}

.progress-bar-fill {
  height: 100%;
  background-color: #0F0;
  transition: width 0.2s linear;
}

.select-option {
  text-align: center;
  margin: 40px 0 20px 0;
  color: #FFF;
  font-weight: bold;
}

.cli-menu {
  list-style: none;
  padding: 0;
  margin: 0 auto;
  width: fit-content;
}

.cli-menu li {
  margin-bottom: 8px;
  text-align: flex-start;
}

.cli-option {
  color: #0F0;
  text-decoration: none;
  transition: color 0.2s, text-shadow 0.2s;
}

.cli-option:hover {
  color: #00FFFF;
  text-shadow: 0 0 5px #00FFFF;
  cursor: pointer;
}

.cli-option.clickable {
  cursor: pointer;
}

.cli-prompt {
  margin-top: 50px;
  color: #0F0;
}

.cursor {
  animation: blink 1s step-end infinite;
  display: inline-block;
  vertical-align: bottom;
}

@keyframes blink {

  from,
  to {
    opacity: 0;
  }

  50% {
    opacity: 1;
  }
}

.help-output,
.credits-output {
  margin-top: 20px;
  padding: 15px;
  border: 1px dashed #0F0;
  background-color: rgba(0, 50, 0, 0.3);
  color: #FFF;
}

.help-output p,
.credits-output p {
  margin: 5px 0;
}

.container-column {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  align-content: center;
  justify-content: center;
}

.green-text {
  color: #0F0;
}

.help-output .cli-button,
.credits-output .cli-button {
  margin-top: 10px;
}
</style>