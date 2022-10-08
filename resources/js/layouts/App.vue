<template>

    <nav class="navbar navbar-expand-sm bg-dark navbar-dark">
        <router-link class="navbar-brand" :to="{name :'Home' }">Home </router-link>
        <ul class="navbar-nav">
            <li class="nav-item">
                <router-link class="text-white" :to="{name : 'Login' }" v-if="$store.getters.getToken == 0">Login</router-link>
            </li>
            <li class="nav-item">
                <router-link class="text-white ml-2" :to="{name : 'Register' }" v-if="$store.getters.getToken == 0"> Register</router-link>
            </li>
            <li class="nav-item">
                <router-link class="text-white ml-2" :to="{name : 'Dashboard' }" v-if="$store.getters.getToken != 0"> Dashboard</router-link>
            </li>
            
 
        </ul>
        <div style="margin-left:85%">
            <a class="navbar-brand" @click="logout" v-if="$store.getters.getToken != 0">Logout </a>
        </div>
        
              
         
    </nav>

    <router-view></router-view>

</template>
<script>
    import { useRouter } from "vue-router"
    import { useStore } from 'vuex'
    export default{
        setup(){
            const router = useRouter();
            const store = useStore();

            function logout(){
                store.dispatch('removeToken');
                router.push({name:'Home'})
            }
          

            return {
                logout
                
            }
        }
    }
</script>