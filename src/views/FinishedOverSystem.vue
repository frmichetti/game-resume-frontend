<template>
    <div class="container py-4" style="margin-top: 50px">
        <h1>Finished over System</h1>
        
        <div class="container-fluid">
            <div class="row row-cols-3">
                <div class="col" v-for="stat,idx in stats" :key="idx">
                            <div class="card text-white bg-dark mb-3" style="max-width:100%">
                                <div class="card-header">{{stat.system}}</div>
                                    <div class="card-body">
                                        <h5 class="card-title">Total of Games: {{stat.total_of_games}}</h5>
                                        <p class="card-text">Games Finished: {{stat.finished_cnt}}</p>
                                        
                                        <div class="progress">
                                            <div class="progress-bar progress-bar-striped progress-bar-animated" :class="statusColor(stat.percentual)"
                                                role="progressbar" :aria-valuenow="stat.percentual" aria-valuemin="0" aria-valuemax="100" :style="{width: `${Math.round(stat.percentual)}%`}">
                                            {{`${Math.round(stat.percentual)}%`}}
                                            </div>
                                        </div>
                                    </div>
                            </div>
                </div>                
            </div>




        </div>
        

        
    </div>    
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {stats: []};
    },
    async mounted() {
        const result = await axios.get(`${process.env.VUE_APP_BACKEND_SERVER}/statistics?from=finished_over_system`);
        this.stats = result.data.result;        
    },
    methods: {
        statusColor(percent) {
            let clazz;
            switch (true) {
                case (percent <= 20):
                    clazz = 'bg-danger'
                    break;              
                case (percent >= 90):
                    clazz = 'bg-success'
                    break;                               
                case (percent <= 50):
                    clazz = 'bg-warning'
                    break    
                default:
                    clazz = 'bg-info'
                    break;
            }
            return clazz
        }
    }
}
</script>

<style>

</style>
