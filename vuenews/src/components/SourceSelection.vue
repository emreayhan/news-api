<template>
    <div class='jumbotron'>
        <h2><span  class='glyphicon glyphicon-list-alt'>News List</span></h2>
        <h4>Select New Source</h4>
        <select class='form-control' v-on:change='sourceChanged'>
        <option :value="source.id" v-for='source in sources'>{{source.name}}</option>
        </select>
        <br>
        <div v-if='source'>
            <h6>{{source.description}}</h6>
            <a :href="source.url" clas='btn btn-primary' target="_blank">Go To {{source.name}} Website</a>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                sources:[],
                source:''
            }
        },
        methods:{
            sourceChanged(e){
                for(let i = 0; i<this.sources.length;i++){
                    if(this.sources[i].id == e.target.value){
                        this.source = this.sources[i]
                    }
                }
                this.$emit('sourceChanged',e.target.value)
            }
        },
        created(){
            this.$http.get('https://newsapi.org/v1/sources?languages=en')
            .then(response => {
                this.sources = response.data.sources;
            });
        }
    }
</script>

<style scoped>

</style>