<template>
  <div class="terminal-window">
    <div class="terminal-header">
      <span class="terminal-title">EJCM@portfolio:~</span>
      <div class="terminal-controls">
        <button class="control-btn minimize">-</button>
        <button class="control-btn maximize">⬜</button>
        <button class="control-btn close">✕</button>
      </div>
    </div>
    <div class="terminal-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
/* Estilos para el marco de la terminal */
.terminal-window {
  background-color: #000;
  border: 2px solid #0F0;
  /* Borde verde brillante, como la imagen */
  border-radius: 8px;
  width: 100%;
  max-width: 90%;
  margin: 40px auto;
  box-shadow: 0 0 20px rgba(0, 255, 0, 0.7);
  /* Glow verde más intenso */
  font-family: 'VT323', 'Consolas', 'Monaco', monospace;
  /* Considera fuentes como VT323 o Press Start 2P para un look más retro-terminal */
  font-size: 1.1em;
  /* Un poco más grande para leer mejor los caracteres */
  color: #0F0;
  /* Texto verde brillante por defecto */
  line-height: 1.2;
  /* Espacio entre líneas para ASCII art */
  min-height: 85vh;
}

/* Estilos para la barra de título de la terminal */
.terminal-header {
  background-color: #000;
  /* Fondo negro */
  padding: 8px 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #0F0;
  /* Borde inferior verde */
}

.terminal-title {
  color: #0F0;
  /* Título verde */
  font-size: 1em;
}

.terminal-controls {
  display: flex;
  gap: 5px;
}

/* Estilos para los botones de control (min, max, close) */
.control-btn {
  background: none;
  border: 1px solid #0F0;
  /* Bordes verdes */
  color: #0F0;
  /* Texto verde */
  width: 20px;
  height: 20px;
  border-radius: 3px;
  cursor: pointer;
  font-size: 0.8em;
  line-height: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
  transition: background-color 0.2s, color 0.2s;
}

.control-btn.close:hover {
  background-color: #FF5F56;
  color: #000;
  border-color: #FF5F56;
}

.control-btn.minimize:hover {
  background-color: #FFBD2E;
  color: #000;
  border-color: #FFBD2E;
}

.control-btn.maximize:hover {
  background-color: #27C93F;
  color: #000;
  border-color: #27C93F;
}

.terminal-content {
  padding: 10px 20px;
  min-height: 400px;
  white-space: pre-wrap;
  /* Mantiene saltos de línea y espacios tal cual, crucial para ASCII art */
  overflow-x: hidden;
  /* Para permitir scroll si hay mucho contenido */
  scroll-behavior: smooth;
  scrollbar-width: none;
  /* Para navegadores que soportan esta propiedad */
  max-height: calc(90vh - 150px);
  /* Ajusta si es necesario */
  width: 100%;
}
</style>