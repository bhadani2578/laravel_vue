<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-sm-6 mt-4">

                <h2>Add Blog</h2>

                <p class="text-danger" v-if="error">{{ error }}</p>

                <form @submit.prevent="submitblog">
                    <div class="form-group">
                        <label for="email">Title:</label>
                        <input type="text" class="form-control" id="email" v-model="form.title">
                    </div>
                   
                     <div class="form-group">
                        <label for="password">Description:</label>
                        <textarea class="form-control" id="password" v-model="form.desc"></textarea>
                    </div>
                    <button type="submit" class="btn btn-primary">Save</button>
                </form>
            </div>
        </div>
    </div>
</template>
<script>
    import { reactive,ref } from 'vue'
    import { useRouter } from "vue-router"
    import { useStore } from 'vuex'
    export default{
        setup(){
            const router = useRouter()
            const store = useStore()

            let form = reactive({
                title: '',
                desc: ''
            });
            let error = ref('')

            const submitblog = async() =>{
                await axios.post('/api/addblog',form).then(res=>{
                    if(res.data.success){
                       
                        router.push({name:'Dashboard'})
                    }else{
                        error.value = res.data.message;
                    }
                })
            }
            return{
                form,
                submitblog,
                error
            }
        }
    }
</script>
