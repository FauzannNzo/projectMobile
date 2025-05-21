<script setup>
import axios from 'axios';
import { onMounted, reactive } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();

const postId = route.params.id;
const state = reactive({
    post: Object
})

onMounted(async () => {
    try {
        const response = await axios.get(` http://localhost/belajar-api/get-all-data.php/?id=${postId}`);
        state.post = response.data;
    } catch (error) {
        console.log("Error while fetching: ", error);
    }
})
</script>

<template>
    <div class="view-page">
        <div class="view-container">
            <div class="view-header">
                <h1>Detail Siswa</h1>
                <p>Informasi lengkap data siswa</p>
            </div>

            <div class="view-content">
                <div class="info-group">
                    <label>Nomor</label>
                    <div class="info-value">{{ state.post.student_no }}</div>
                </div>

                <div class="info-group">
                    <label>Nama</label>
                    <div class="info-value">{{ state.post.student_name }}</div>
                </div>

                <div class="info-group">
                    <label>Kelas</label>
                    <div class="info-value">{{ state.post.student_class }}</div>
                </div>
            </div>

            <div class="view-actions">
                <RouterLink :to="`/posts`" class="btn btn-back">Kembali</RouterLink>
            </div>
        </div>
    </div>
</template>

<style scoped>
.view-page {
    min-height: 100vh;
    background: white;
    padding: 2rem;
    display: flex;
    align-items: center;
    justify-content: center;
}

.view-container {
    background: white;
    padding: 2rem;
    border-radius: 12px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
    width: 100%;
    max-width: 500px;
    animation: fadeIn 0.8s ease-out;
}

.view-header {
    text-align: center;
    margin-bottom: 2rem;
}

.view-header h1 {
    color: #2c3e50;
    font-size: 1.8rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
}

.view-header p {
    color: #6c757d;
    font-size: 0.95rem;
}

.view-content {
    margin-bottom: 2rem;
}

.info-group {
    margin-bottom: 1.5rem;
}

.info-group:last-child {
    margin-bottom: 0;
}

label {
    display: block;
    margin-bottom: 0.5rem;
    color: #2c3e50;
    font-weight: 500;
    font-size: 0.95rem;
}

.info-value {
    padding: 0.8rem 1rem;
    background: #f8f9fa;
    border: 1px solid #e9ecef;
    border-radius: 8px;
    font-size: 1rem;
    color: #2c3e50;
    font-weight: 500;
}

.view-actions {
    display: flex;
    justify-content: center;
    margin-top: 2rem;
}

.btn {
    padding: 0.8rem 2rem;
    border-radius: 8px;
    font-weight: 500;
    font-size: 0.95rem;
    transition: all 0.3s ease;
    cursor: pointer;
    border: none;
    text-decoration: none;
    text-align: center;
}

.btn-back {
    background: #f8f9fa;
    color: #2c3e50;
    border: 1px solid #e9ecef;
}

.btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
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
    .view-page {
        padding: 1rem;
    }

    .view-container {
        padding: 1.5rem;
    }

    .view-header h1 {
        font-size: 1.5rem;
    }

    .btn {
        padding: 0.7rem 1.5rem;
        font-size: 0.9rem;
    }
}
</style>