<script setup>
import { onMounted, reactive } from 'vue';
import { RouterLink, useRouter } from 'vue-router';
import axios from 'axios';
import Post from '@/components/Post.vue';

const router = useRouter();
const state = reactive({
    posts: []
})

const handleLogout = () => {
    if (confirm('Apakah Anda yakin ingin logout?')) {
        localStorage.removeItem('isLoggedIn');
        router.push('/');
    }
};

onMounted(async () => {
  try {
    const response = await axios.get(' http://localhost/belajar-api/get-all-data.php');
    state.posts = response.data;
  } catch (error) {
    console.error('Error fetching jobs:', error);
  }
});
</script>

<template>
  <div class="posts-page">
    <div class="content">
      <div class="header">
        <h1>Data Siswa</h1>
        <div class="actions">
          <RouterLink :to="`/home`" class="nav-button">Beranda</RouterLink>
          <RouterLink :to="`/posts/add`" class="action-button">Tambah</RouterLink>
          <button @click="handleLogout" class="nav-button">Logout</button>
        </div>
      </div>

      <div class="table-container">
        <div class="table-responsive">
          <table>
            <thead>
              <tr>
                <th>No</th>
                <th>Name</th>
                <th>Class</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody>
              <Post v-for="post in state.posts" :key="post.id" :post="post"/>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.posts-page {
    min-height: 100vh;
    background: white;
    padding: 1rem;
}

.content {
    max-width: 1200px;
    margin: 0 auto;
    animation: fadeIn 0.8s ease-out;
}

.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 2rem;
    flex-wrap: wrap;
    gap: 1rem;
}

h1 {
    font-size: 2rem;
    font-weight: 700;
    color: #2c3e50;
    margin: 0;
}

.actions {
    display: flex;
    gap: 0.5rem;
    flex-wrap: wrap;
}

.nav-button, .action-button {
    display: inline-block;
    padding: 0.8rem 1.2rem;
    border-radius: 12px;
    text-decoration: none;
    font-weight: 500;
    font-size: 0.9rem;
    transition: all 0.3s ease;
    cursor: pointer;
    border: 1px solid #e9ecef;
    white-space: nowrap;
}

.nav-button {
    background: #f8f9fa;
    color: #2c3e50;
}

.action-button {
    background: #2c3e50;
    color: white;
    box-shadow: 0 4px 15px rgba(44, 62, 80, 0.1);
    border: none;
}

.nav-button:hover, .action-button:hover {
    transform: translateY(-2px);
}

.nav-button:hover {
    background: #e9ecef;
}

.action-button:hover {
    box-shadow: 0 6px 20px rgba(44, 62, 80, 0.15);
}

.table-container {
    background: white;
    border-radius: 12px;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
    overflow: hidden;
    margin-top: 1rem;
    padding: 0.5rem;
}

.table-responsive {
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
}

table {
    width: 100%;
    border-collapse: separate;
    border-spacing: 0 0.5rem;
    min-width: 600px;
}

th {
    background: #f8f9fa;
    color: #2c3e50;
    font-weight: 600;
    text-align: left;
    padding: 1rem;
    border-bottom: 2px solid #e9ecef;
    font-size: 0.9rem;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    white-space: nowrap;
}

td {
    padding: 1rem;
    border-bottom: 1px solid #e9ecef;
    color: #2c3e50;
    font-weight: 500;
    font-size: 0.9rem;
    vertical-align: middle;
    background: white;
}

tr {
    margin-bottom: 0.5rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.02);
    border-radius: 8px;
}

tr:hover {
    background: #f8f9fa;
}

tr:hover td {
    color: #1a2530;
    background: #f8f9fa;
}

tr:last-child td {
    border-bottom: none;
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

/* Tablet */
@media (max-width: 768px) {
    .posts-page {
        padding: 0.8rem;
    }

    .header {
        flex-direction: column;
        align-items: stretch;
        text-align: center;
        gap: 1rem;
    }

    h1 {
        font-size: 1.8rem;
    }

    .actions {
        justify-content: center;
    }

    .table-container {
        margin-top: 1rem;
        padding: 0.5rem;
    }

    .nav-button, .action-button {
        padding: 0.7rem 1rem;
        font-size: 0.85rem;
    }
}

/* Mobile */
@media (max-width: 480px) {
    .posts-page {
        padding: 0.5rem;
    }

    h1 {
        font-size: 1.5rem;
    }

    .actions {
        flex-direction: column;
        width: 100%;
    }

    .nav-button, .action-button {
        width: 100%;
        text-align: center;
        padding: 0.8rem;
    }

    .table-container {
        margin-top: 0.8rem;
        padding: 0.3rem;
    }

    th, td {
        padding: 0.8rem;
        font-size: 0.85rem;
    }
}
</style>