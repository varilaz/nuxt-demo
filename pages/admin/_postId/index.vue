<template>
    <div class="admin-post-page">
        <section>
            <AdminPostForm :post="loadedPost" @submit="onSubmitted" />
        </section>

    </div>
</template>

<script>
import AdminPostForm from '@/components/Admin/AdminPostForm'
import axios from 'axios'
export default {
    layout: 'admin',
    middleware: ['check-auth','auth'],
    components: {
        AdminPostForm
    },
     asyncData(context){
        return axios.get(process.env.baseUrl + '/posts/' + context.params.postId + '.json')
        .then(res => {
            return {
            loadedPost: {...res.data, id:context.params.postId}
            }
        })
        .catch(e => context.error(e))
    },
    methods: {
        onSubmitted(editedPost){
         this.$store.dispatch('editPost', editedPost)
         .then(() => {
             this.$router.push('/admin');
         })
        }
    }
    
}
</script>

<style scoped>
   .admin-post-page {
        width: 90%;
        margin: 20px auto;
    }
    
    @media (min-width: 768px){
        .admin-post-page{
            width: 500px;
        }
    }
</style>