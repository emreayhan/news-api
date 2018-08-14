<template>
  <div class='container' id='app'>
    <source-selection v-on:sourceChanged='sourceChanged'></source-selection>
    <news-list :source='source'></news-list>
  </div>
</template>

<script>
import SourceSelection from './components/SourceSelection';
import NewsList from './components/NewsList';
  export default {
    components:{
      'source-selection' : SourceSelection,
      'news-list' : NewsList
    },
    data(){
      return{
        source:''
      }
    },
    methods:{
      sourceChanged(source){
        this.source=source
      }
    }
  }
</script>

<style scoped>
#app{
  padding-top: 20px
}
</style>