<template>
    <NuxtLink to="/" class="cli-button"><i class="bi bi-arrow-left-short"></i></NuxtLink>
    <div class="about-page mt-4">
        <p class="cli-command mb-2">$ EJCM@root</p>
        <div class="typewriter-container">
            <div v-for="(line, index) in typewriterLines" :key="index" :style="{ '--delay': index * 0.1 + 's' }"
                class="typewriter-line">
                {{ line }}
            </div>
        </div>

        <div class="info-sections">
            <div class="section-box">
                <h3 class="section-title">HABILIDADES</h3>
                <br>
                <p class="section-content">
                    <span class="green-text">Lenguajes y Frameworks:
                    </span> Python (Django, DRF, FastApi), JavaScript, Vue.js, Bash, Nuxt.
                </p>
                <p class="section-content">
                    <span class="green-text">Bases de Datos:</span> PostgreSQL, SQLite, IncoDB.
                </p>
                <p class="section-content">
                    <span class="green-text">Herramientas:</span> Git (GitHub), VS Code, Trello (Kanban), npm,
                    Capacitor, Vite.
                </p>
                <p class="section-content">
                    <span class="green-text">Cloud & Servicios:</span> AWS-S3, Render, Supabase, Vercel.
                </p>
            </div>

            <div class="section-box">
                <h3 class="section-title">EDUCACIÓN</h3>
                <br>
                <p class="section-content">
                    <span class="green-text">TSU en Informática:</span> UPTAIET Táchira 2024.
                </p>
                <p class="section-content">
                    <span class="green-text">Ingenieria en Informatica:</span> En curso - Diciembre 2026 .

                </p>
            </div>
            <div class="section-box">
                <h3 class="section-title">IDIOMAS</h3>
                <br>
                <p class="section-content">
                    <span class="green-text">Español:</span> Nativo.
                </p>
                <p class="section-content">
                    <span class="green-text">Inglés:</span> Básico / Intermedio (Uso profesional para lectura de
                    documentación técnica).
                </p>
            </div>
        </div>
        <NuxtLink to="/" class="start-button cli-button w-100 text-center p-2">Volver</NuxtLink>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

// Información que aparecerá con el efecto de máquina de escribir
const whoamiText = [
    "Eber J Colmenares M", "Desarrollador Web Fullstack - Especialista en Backend",
    "Construyo sistemas con una lógica clara y un enfoque minimalista, asegurando una documentación trazable y propuestas comprensibles para clientes técnicos y no técnicos. Mi trabajo se centra en la funcionalidad y eficiencia, siempre partiendo del modelado de la Base de datos hasta una presentación visual precisa y funcional."
];

const typewriterLines = ref([]);

const typeWriterEffect = async () => {
    for (const line of whoamiText) {
        let typedLine = '';
        for (const char of line) {
            typedLine += char;
            typewriterLines.value.splice(typewriterLines.value.length - 1, 1, typedLine);
            await new Promise(resolve => setTimeout(resolve, 10)); // Ajusta la velocidad aquí
        }
        typewriterLines.value.push(''); // Añade una nueva línea para el siguiente texto
        await new Promise(resolve => setTimeout(resolve, 900)); // Pausa entre líneas
    }
};

onMounted(() => {
    typewriterLines.value.push(''); // Inicializa con una línea vacía
    typeWriterEffect();
});
</script>

<style scoped>
.about-page {
    font-family: 'Consolas', monospace;
    color: #0F0;
    white-space: pre-wrap;
}

.cli-command {
    font-size: 1.1rem;
    margin-bottom: 20px;
}

/* --- Efecto de máquina de escribir --- */
.typewriter-container {
    margin-bottom: 30px;
    width: 90%;
    /* Limita el ancho del contenedor al 90% */
    max-width: 100%;
    /* Evita que crezca demasiado en pantallas grandes */
}

.typewriter-line {
    display: block;
    /* Cambiamos a block para que ocupe todo el ancho */
    overflow: hidden;
    border-right: 0.15em solid transparent;
    width: 0;
    animation: typing 2s steps(40, end) forwards;
    animation-delay: var(--delay);
}

.typewriter-line:last-child {
    border-right: 0.15em solid #0F0;
    animation: typing 2s steps(40, end) forwards, blink-caret 0.75s step-end infinite;
    animation-delay: var(--delay);
}

@keyframes typing {
    from {
        width: 0
    }

    to {
        width: 100%
    }
}

@keyframes blink-caret {

    from,
    to {
        border-color: transparent
    }

    100% {
        border-color: #0F0;
    }
}

/* -- Fin del efecto -- */

.info-sections {
    display: flex;
    flex-wrap: wrap;
    gap: 30px;
    margin-top: 20px;
}

.section-box {
    border: 1px dashed #00FFFF;
    padding: 20px;
    flex: 1;
    min-width: 300px;
    background-color: rgba(0, 100, 100, 0.1);
}

.section-title {
    color: #00FFFF;
    text-transform: uppercase;
    margin-top: 0;
    border-bottom: 1px dashed #00FFFF;
    padding-bottom: 5px;
}

.section-content {
    color: #FFF;
    margin-bottom: 15px;
}

.green-text {
    color: #0F0;
}
</style>