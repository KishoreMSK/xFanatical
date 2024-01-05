<template >
    <v-card
      class="mx-auto"
      max-width="254"
      min-width="200"
      @click="handleClick(book.link)"
    >
      <v-img
        :src=book.cover
        height="200px"
      ></v-img>
  
      <v-card-title>
        {{book.title}}
      </v-card-title>
  
      <v-card-subtitle>
        {{ book.author }}
      </v-card-subtitle>
  
      <V-card-text>{{ book.year }}</V-card-text>        
    </v-card>
</template>

<script>
export default{
    name: 'CardComponent',
    props:{
        book: Object
    },
    data(){
        return{
            // bookData: this.book
        }
    },
    mounted(){
        // console.log(this.book);
    },
    methods:{
        handleClick(link){
            window.open(link, '_blank');
        }
    }
}

</script>

<style scoped>

</style>