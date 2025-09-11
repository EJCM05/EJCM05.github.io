<template>
    <div class="contact-page">
        <p class="cli-command">$ mail -s</p>
        <p>Si quieres contactarme, por favor llena el siguiente formulario.</p>
        <div v-if="successMessage" class="success-message">
            <p>Email enviado correctamente!</p>
            <p>Gracias por tu mensaje. Me pondré en contacto contigo pronto.</p>
        </div>
        <div v-else class="contact-form">
            <div v-if="isLoading" class="loading-message">
                <span class="loading-prompt">enviando email...</span>
                <span class="cursor">_</span>
            </div>

            <div v-else>
                <div class="input-line">
                    <label for="name">Tu Nombre:</label>
                    <input type="text" id="name" v-model="form.name" @keyup.enter="focusEmail" ref="nameInput">
                </div>

                <div class="input-line">
                    <label for="email">Tu Correo Electrónico:</label>
                    <input type="email" id="email" v-model="form.email" @keyup.enter="focusMessage" ref="emailInput">
                </div>

                <div class="input-line">
                    <label for="message">Tu Mensaje:</label>
                    <textarea id="message" v-model="form.message" ref="messageInput" rows="5"></textarea>
                </div>

                <button @click="sendEmail" class="send-button cli-button" :disabled="isLoading">ENVIAR</button>
            </div>

            <div v-if="errorMessage" class="error-message">
                <p>Error: No se pudo enviar el email.</p>
                <p>{{ errorMessage }}</p>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import emailjs from '@emailjs/browser';

// Usamos useRuntimeConfig para obtener las variables de entorno
const runtimeConfig = useRuntimeConfig();

const form = ref({
    name: '',
    email: '',
    message: ''
});

const isLoading = ref(false); // <--- DEBE ESTAR AQUÍ
const successMessage = ref(false);
const errorMessage = ref(null);

// Referencias para controlar el foco en los inputs
const nameInput = ref(null);
const emailInput = ref(null);
const messageInput = ref(null);

const focusEmail = () => {
    emailInput.value.focus();
};
const focusMessage = () => {
    messageInput.value.focus();
};

const sendEmail = async () => {
    if (!form.value.name || !form.value.email || !form.value.message) {
        errorMessage.value = "All fields are required.";
        return;
    }

    isLoading.value = true;
    errorMessage.value = null;

    // Accedemos a las variables desde runtimeConfig
    const serviceId = runtimeConfig.public.emailJsServiceId;
    const templateId = runtimeConfig.public.emailJsTemplateId;
    const publicKey = runtimeConfig.public.emailJsPublicKey;

    try {
        await emailjs.send(serviceId, templateId, form.value, publicKey);
        successMessage.value = true;
        form.value = { name: '', email: '', message: '' };
    } catch (error) {
        errorMessage.value = error.text || "Something went wrong. Please try again.";
        console.error("EmailJS Error:", error);
    } finally {
        isLoading.value = false;
    }
};
</script>

<style scoped>
.contact-page {
    font-family: 'Consolas', 'Monaco', monospace;
    color: #0F0;
    padding: 20px;
}

.cli-command {
    font-size: 1.1rem;
    margin-bottom: 20px;
}

.contact-form {
    width: 100%;
}

.input-line {
    margin-bottom: 20px;
}

.input-line label {
    display: block;
    font-weight: bold;
    color: #00FFFF;
    margin-bottom: 5px;
}

.input-line input,
.input-line textarea {
    width: 100%;
    padding: 8px;
    background-color: transparent;
    border: 1px dashed #0F0;
    color: #FFF;
    font-family: 'Consolas', monospace;
    font-size: 1em;
    resize: vertical;
}

.input-line input:focus,
.input-line textarea:focus {
    outline: none;
    border-color: #00FFFF;
    box-shadow: 0 0 5px rgba(0, 255, 255, 0.5);
}

.send-button {
    width: auto;
    padding: 10px 20px;
    background-color: transparent;
    color: #0F0;
    border: 1px dashed #0F0;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.2s ease;
}

.send-button:hover:not(:disabled) {
    background-color: #0F0;
    color: #000;
    box-shadow: 0 0 10px rgba(0, 255, 0, 0.5);
}

.send-button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
}

.loading-message,
.success-message,
.error-message {
    padding: 20px;
    border: 1px dashed #00FFFF;
    background-color: rgba(0, 255, 255, 0.05);
    margin-top: 20px;
}

.success-message {
    color: #27C93F;
}

.error-message {
    color: #FF5F56;
}

.loading-message {
    color: #00FFFF;
}

.cursor {
    animation: blink 1s step-end infinite;
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
</style>