<script setup>
import { RouterLink } from 'vue-router';
</script>

<template>
    <div class="minimal-page">
        <div class="content">
            <h1>Selamat Datang!</h1>
            <RouterLink :to="`/posts`" class="enter-button">
                Masuk ke Sistem
            </RouterLink>
        </div>
    </div>
</template>

<style scoped>
.minimal-page {
    min-height: 100vh;
    background: white;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 2rem;
}

.content {
    text-align: center;
    animation: fadeIn 0.8s ease-out;
}

h1 {
    font-size: 3rem;
    font-weight: 700;
    color: #2c3e50;
    margin-bottom: 2rem;
    line-height: 1.2;
}

.enter-button {
    display: inline-block;
    background: #2c3e50;
    color: white;
    padding: 1rem 3rem;
    border-radius: 12px;
    text-decoration: none;
    font-weight: 500;
    font-size: 1.1rem;
    transition: all 0.3s ease;
    box-shadow: 0 4px 15px rgba(44, 62, 80, 0.1);
}

.enter-button:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(44, 62, 80, 0.15);
}

@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@media (max-width: 480px) {
    h1 {
        font-size: 2.5rem;
    }

    .enter-button {
        padding: 0.8rem 2.5rem;
    }
}
</style>