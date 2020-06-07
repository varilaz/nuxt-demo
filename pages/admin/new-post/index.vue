<template>
    <div class="admin-new-post-page">
        <section>
         <AdminPostForm  @submit="onSubmitted"/>
        </section>
    </div>
</template>

<script>
import AdminPostForm from '@/components/Admin/AdminPostForm'
import axios from 'axios';
export default {
    layout: 'admin',
    middleware: ['check-auth','auth'],
    components: {
        AdminPostForm
    },
    methods: {
        onSubmitted(postData){
           this.$store.dispatch('addPost', postData)
           .then(() => {
               this.$router.push("/admin");
           })
        }
    }
}
</script>

<style scoped>
    .admin-new-post-page {
        width: 90%;
        margin: 20px auto;
    }
    
    @media (min-width: 768px){
        .admin-new-post-page{
            width: 500px;
        }
    }
</style>