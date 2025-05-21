<script setup>
import axios from 'axios';
import { defineProps } from 'vue';
import { RouterLink, useRouter } from 'vue-router';

const router = useRouter();

const props = defineProps({
    post: Object
});

const deletePost = async (deletedId) => {
    try {
    const confirm = window.confirm('Are you sure you want to delete this posts?');
    if (confirm) {
        const res = await axios.delete(`http://localhost/belajar-api/delete-data.php?student_id=${deletedId}`);
        console.log('Delete success:', res.data);
        router.push('/');
    }
    } catch (error) {
    console.error("Error deleting post: ", error.response?.data || error.message);
    }
}
</script>

<template>
    <tr>
        <td>{{ post.student_no }}</td>
        <td>{{ post.student_name }}</td>
        <td>{{ post.student_class }}</td>
        <td>
            <RouterLink :to="`/posts/${post.student_id}`" class="btn btn-green">View</RouterLink>
            <RouterLink :to="`/posts/edit/${post.student_id}`" class="btn btn-blue">Update</RouterLink>
            <RouterLink :to="`/posts/${post.student_id}`" @click="deletePost(post.student_id)" class="btn btn-red">Delete</RouterLink>
           
        </td>
    </tr>
</template>

<style scoped>
td {
    color: #2c3e50 !important;
    font-weight: 500;
}

.btn {
    display: inline-block;
    padding: 0.5rem 1rem;
    margin: 0 0.25rem;
    border-radius: 6px;
    text-decoration: none;
    font-weight: 500;
    font-size: 0.9rem;
    transition: all 0.3s ease;
    border: none;
    cursor: pointer;
}

.btn-green {
    background: #2ecc71;
    color: white;
}

.btn-blue {
    background: #3498db;
    color: white;
}

.btn-red {
    background: #e74c3c;
    color: white;
}

.btn:hover {
    transform: translateY(-2px);
    opacity: 0.9;
}
</style>