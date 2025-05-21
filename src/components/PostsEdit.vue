<script setup>
import axios from 'axios';
import { onMounted, reactive } from 'vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();

const postId = route.params.id;

const form = reactive({
    student_no: '',
    student_name: '',
    student_class: ''
})

onMounted(async () => {
    try {
        const response = await axios.get(`http://localhost/belajar-api/get-all-data.php/?id=${postId}`);
        form.student_no = response.data.student_no;
        form.student_name = response.data.student_name;
        form.student_class = response.data.student_class;
    } catch (error) {
        console.log("Error fetching post", error);
    }
})

const handleSubmit = async () => {
    const updatePost = {
        student_id: postId,
        student_no: form.student_no,
        student_name: form.student_name,
        student_class: form.student_class
    }

    try {
        const response = await axios.put(`http://localhost/belajar-api/update-data.php`, updatePost);
        console.log(response);
        router.push('/posts');
    } catch (error) {
        console.error("Error updating post", error);
    }
}
</script>

<template>
    <div class="form-page">
        <div class="form-container">
            <div class="form-header">
                <h1>Edit Data Siswa</h1>
                <p>Silakan edit data siswa yang ada</p>
            </div>

            <form @submit.prevent="handleSubmit">
                <div class="form-group">
                    <label for="no">Nomor</label>
                    <input 
                        v-model="form.student_no" 
                        type="text" 
                        id="no" 
                        class="form-control"
                        placeholder="Masukkan nomor siswa"
                        required>
                </div>

                <div class="form-group">
                    <label for="name">Nama</label>
                    <input 
                        v-model="form.student_name" 
                        type="text" 
                        id="name" 
                        class="form-control"
                        placeholder="Masukkan nama siswa"
                        required>
                </div>

                <div class="form-group">
                    <label for="class">Kelas</label>
                    <input
                        v-model="form.student_class" 
                        type="text"
                        id="class" 
                        class="form-control"
                        placeholder="Masukkan kelas siswa"
                        required>
                </div>

                <div class="form-actions">
                    <button type="submit" class="btn btn-submit">Simpan Perubahan</button>
                    <RouterLink :to="`/posts`" class="btn btn-back">Kembali</RouterLink>
                </div>
            </form>
        </div>
    </div>
</template>

<style scoped>
.form-page {
    min-height: 100vh;
    background: white;
    padding: 2rem;
    display: flex;
    align-items: center;
    justify-content: center;
}

.form-container {
    background: white;
    padding: 2rem;
    border-radius: 12px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
    width: 100%;
    max-width: 500px;
    animation: fadeIn 0.8s ease-out;
}

.form-header {
    text-align: center;
    margin-bottom: 2rem;
}

.form-header h1 {
    color: #2c3e50;
    font-size: 1.8rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
}

.form-header p {
    color: #6c757d;
    font-size: 0.95rem;
}

.form-group {
    margin-bottom: 1.5rem;
}

label {
    display: block;
    margin-bottom: 0.5rem;
    color: #2c3e50;
    font-weight: 500;
    font-size: 0.95rem;
}

input {
    width: 100%;
    padding: 0.8rem 1rem;
    border: 1px solid #e9ecef;
    border-radius: 8px;
    font-size: 0.95rem;
    color: #2c3e50 !important;
    transition: all 0.3s ease;
    background-color: white;
}

input:focus {
    outline: none;
    border-color: #3498db;
    box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
}

input::placeholder {
    color: #adb5bd;
}

input:-webkit-autofill,
input:-webkit-autofill:hover,
input:-webkit-autofill:focus {
    -webkit-text-fill-color: #2c3e50;
    -webkit-box-shadow: 0 0 0px 1000px white inset;
    transition: background-color 5000s ease-in-out 0s;
}

.form-actions {
    display: flex;
    gap: 1rem;
    margin-top: 2rem;
}

.btn {
    padding: 0.8rem 1.5rem;
    border-radius: 8px;
    font-weight: 500;
    font-size: 0.95rem;
    transition: all 0.3s ease;
    cursor: pointer;
    border: none;
    text-decoration: none;
    text-align: center;
    flex: 1;
}

.btn-submit {
    background: #3498db;
    color: white;
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
    .form-page {
        padding: 1rem;
    }

    .form-container {
        padding: 1.5rem;
    }

    .form-header h1 {
        font-size: 1.5rem;
    }

    .btn {
        padding: 0.7rem 1.2rem;
        font-size: 0.9rem;
    }
}
</style>