<template>
    <div class="projects-page">
        <p class="cli-command">$ ls -la</p>

        <div v-if="loading" class="loading-message">
            <span class="loading-prompt">Fetching projects from GitHub...</span>
            <span class="cursor">_</span>
        </div>

        <div v-if="error" class="error-message">
            <p class="error-prompt">Error: Could not retrieve projects.</p>
            <p class="error-prompt">{{ error }}</p>
        </div>

        <ul v-if="!loading && !error" class="projects-list">
            <li v-for="project in publicProjects" :key="project.id" class="project-item">
                <a :href="project.html_url" target="_blank" rel="noopener noreferrer" class="project-link">
                    <span class="file-name">{{ project.name }}</span>
                </a>
                <p class="project-description">{{ project.description || 'No description provided.' }}</p>
                <p class="project-meta">
                    <span class="project-language">Language: {{ project.language || 'N/A' }}</span>
                    <span class="project-stars">⭐ {{ project.stargazers_count }}</span>
                    <span class="project-forks">🍴 {{ project.forks_count }}</span>
                </p>
            </li>
        </ul>

        <p v-if="!loading && !error" class="cli-prompt">
            $ root:@EberC:<span class="cursor">_</span>
        </p>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

// Usamos useRuntimeConfig para obtener las variables de entorno
const runtimeConfig = useRuntimeConfig();
const username = runtimeConfig.public.githubUsername;

const publicProjects = ref([]);
const loading = ref(true);
const error = ref(null);

const fetchPublicProjects = async () => {
    try {
        const response = await fetch(`https://api.github.com/users/${username}/repos?type=owner&sort=updated`);
        if (!response.ok) {
            throw new Error(`GitHub API returned status ${response.status}`);
        }
        const data = await response.json();
        publicProjects.value = data.filter(repo => !repo.private);
    } catch (err) {
        error.value = err.message;
        console.error('Failed to fetch GitHub projects:', err);
    } finally {
        loading.value = false;
    }
};

onMounted(() => {
    // La validación ahora es opcional porque useRuntimeConfig garantiza que la variable existe
    fetchPublicProjects();
});
</script>

<style scoped>
.projects-page {
    font-family: 'Consolas', 'Monaco', monospace;
    color: #0F0;
    padding: 20px;
}

.cli-command {
    font-size: 1.1rem;
    margin-bottom: 20px;
}

.loading-message,
.error-message {
    color: #00FFFF;
}

.loading-prompt,
.error-prompt {
    display: inline-block;
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

.projects-list {
    list-style: none;
    padding: 0;
    margin: 0;
}

.project-item {
    border-left: 2px solid #00FFFF;
    padding-left: 10px;
    margin-bottom: 20px;
    transition: all 0.3s ease;
    background-color: rgba(0, 255, 255, 0.05);
}

.project-item:hover {
    border-left-color: #0F0;
    transform: translateX(5px);
    background-color: rgba(0, 255, 0, 0.1);
}

.project-link {
    color: #0F0;
    text-decoration: none;
    font-weight: bold;
}

.project-link:hover {
    color: #00FFFF;
    text-decoration: underline;
}

.file-name {
    font-size: 1.2rem;
    color: #00FFFF;
}

.project-description {
    margin: 5px 0 10px 0;
    color: #FFF;
}

.project-meta {
    font-size: 0.9rem;
    color: #999;
}

.project-meta span {
    margin-right: 15px;
}

.project-language {
    color: #0F0;
}

.project-stars,
.project-forks {
    color: #FFD700;
}

.cli-prompt {
    margin-top: 50px;
    color: #0F0;
}
</style>