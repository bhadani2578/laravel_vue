<template>
    <div class="container">
        <h2>Blogs </h2>
        <div  style="display: flex;">
       
        <button type="button" class="btn btn-danger mt-2" @click="addBlog">Add Blog</button>
        
        </div>
        <div>
            <table>
                <tr>
                    <th>Id</th>
                    <th>Name</th>
                    <th>Description</th>
                </tr>
                <tr v-for="item in this.data" :key="item">
                    <td>{{item['id']}}</td>
                    <td>{{item['title']}}</td>
                    <td>{{item['desc']}}</td>
                </tr>
            </table>
        </div>
    </div>
</template>
<script>
    import { reactive,ref } from 'vue'
    import { useRouter } from "vue-router"
    import { useStore } from 'vuex'
    export default{
         data() {
            return {
                data: [{}],
            }
        },
        created () {
           axios.get('/api/bloglist').then(res=>{
                    if(res.data.success){
                        
                      this.data = res.data.data;
                      console.log(this.data);
                    }else{
                        error.value = res.data.message;
                    }
                })
        },
       
        setup(){
            const router = useRouter();
            const store = useStore();
       
            let data = ref([]);
            function logout(){
                store.dispatch('removeToken');
                router.push({name:'Home'})
            }
            function addBlog(){            
                router.push({name: 'AddBlog'})
            }

             

            return {
                logout,
                addBlog,
                bloglist
                
            }
        }
    }
</script>
