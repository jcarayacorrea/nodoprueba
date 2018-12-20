<template>
  <div>
    
    <table >
      <tr>
        <th>Name</th> <td>{{character.name}}</td>
      </tr>
      <tr>
        <th>Date Of Birth</th> <td>{{character.dateOfBirth}}</td>
      </tr>
      <tr>
        <th>Date Of Death</th> <td>{{character.dateOfDeath}}</td>
      </tr>
      <tr>
        <th>House</th> <td>{{character.dateOfDeath}}</td>
      </tr>
      <tr>
        <th>Genre</th> <td>{{(character.male)?'Male':'Female'}}</td>
      </tr>
       <tr>
        <th>Page Rank</th> <td>{{character.pageRank}}</td>
      </tr>
      <tr>
        <th>Slug</th> <td>{{character.slug}}</td>
      </tr>
      <tr>
        <th>Titles</th> <td v-for="title in character.title">{{title}}</td>
      </tr> 
      <tr>
        <th>Books</th> <td v-for="book in character.books">{{book}}</td>
      </tr> 
       
      
    </table>
    <button @click="back()">Volver</button> 
  </div>
</template>


<script>
  
  import { getACharacter } from '../services/got.service.js'


  export default {
    name: 'detail-component',
    

    /**
     * @description the data block represents all the local variable of this component.
     */
    data () {
      return {
        character: {}
      }
    },

    /**
     * @description the create function is the first one to be execute when the component is being created (see vue js lifecycle).
     */
    created () {
     //this.character = this.$router.params
     let id = this.$route.params.id
      getACharacter(id).then((res)=>{
         
          this.character = res.data;
          console.log(this.character);
        });
     
    },

    /**
     * @description the methods block represents all the local methods of this component.
     */
    methods: {

      /**
       * @description get the detail of a character from the GoT API.
       * @param {string} id. the "_id" of the character that we are going to request.
       * @method goToDetail
       */
      back(){
           this.$router.push({name:'list'});
      }
      
    }
  }
</script>
<style>
  table {
    font-family: arial, sans-serif;
    border-collapse: collapse;
    width: 100%;
  }

  td, th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
  }

  tr:nth-child(even) {
    background-color: #dddddd;
  }
</style>