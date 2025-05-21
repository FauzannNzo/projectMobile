<script setup>
import axios from 'axios';
import { reactive } from 'vue';
import router from '@/router';

const form = reactive({
    username: '',
    password: ''
})

const handleLogin = async () => {
    try {
        const response = await axios.post('http://localhost/belajar-api/login.php', {
            username: form.username,
            password: form.password
        });

        if (response.data.status === 'success') {
            // Store login state
            localStorage.setItem('isLoggedIn', 'true');
            // Redirect to posts page
            router.push('/posts');
        } else {
            alert(response.data.message || 'Invalid');
        }
    } catch (error) {
        console.error('Login error:', error);
        alert('Login failed. Please try again.');
    }
};
</script>

<template>
    <div class="form-page">
        <div class="form-container">
            <div class="form-header">
                <h1>Login</h1>
                <p>Silakan masuk ke akun Anda</p>
            </div>

            <form @submit.prevent="handleLogin">
                <div class="form-group">
                    <label for="username">Username</label>
                    <input 
                        v-model="form.username" 
                        type="text" 
                        id="username" 
                        class="form-control"
                        placeholder="Masukkan username"
                        required>
                </div>

                <div class="form-group">
                    <label for="password">Password</label>
                    <input 
                        v-model="form.password" 
                        type="password" 
                        id="password" 
                        class="form-control"
                        placeholder="Masukkan password"
                        required>
                </div>

                <div class="form-actions">
                    <button type="submit" class="btn btn-submit">Masuk</button>
                </div>
            </form>
        </div>
    </div>
</template>

<style scoped>
.form-page {
    min-height: 100vh;
    background: #f8f9fa;
    padding: 2rem;
    display: flex;
    align-items: center;
    justify-content: center;
}

.form-container {
    background: white;
    padding: 2.5rem;
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
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
}

.form-header p {
    color: #6c757d;
    font-size: 1rem;
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
    color: #2c3e50;
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
