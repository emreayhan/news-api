<template>
    <div class='container'>
        <ul class="media-list">
            <li class="media" v-for='article in articles'>
                <div class="media-left">
                    <a :href="article.url" target="_blank">
                        <img :src="article.urlToImage" class='media-object'>
                    </a>
                </div>
                <div class="media-body">
                    <h4 class='media-heading'>
                        <a :href="article.url" target="_blank">{{article.title}}</a>
                    </h4>
                    <h5><i>by {{article.author}}</i></h5>
                    <p>{{article.description}}</p>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                articles:[]
            }
        },
        props:['source'],
        methods:{
            updataSource(source){
                this.$http.get('http://newsapi.org/v1/articles?source=' + source + '&apiKey=6debe5a5cb8d4e1db5949439993c4153')
            .then(response => {
                this.articles= response.data.articles;
            })
           }
        },
        created(){
            this.updataSource(this.source)
        },
        watch:{
            source(val){
                this.updataSource(val)
            }
        }
    }
</script>

<style scoped>
.media-object{
    width:128px;
    padding: 10px;
}
.media{
    border-top:1px;
    padding-top:20px;
}
</style>