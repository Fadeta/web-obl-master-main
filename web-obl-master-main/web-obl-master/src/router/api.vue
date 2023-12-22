<script>
import Vue from 'vue';
import axios from 'axios';
import VueAxios from 'vue-axios';

Vue.use(VueAxios, axios)
export default {
    name:"dashboard",
    data(){
        return {list:undefined}
    },
    mounted()
    {    
            Vue.axios.get('http:/localhost:4000/users')
            .then((resp) => {
                this.list=resp.data.data
                console.warn(resp.data.data)
            })
    }
}
</script>