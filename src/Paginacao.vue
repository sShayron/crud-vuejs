<template>
  <nav class="pagination">
    <a class="button" v-show="showPreviousButton" @click="goPreviousPage()">Anterior</a>
    <a class="button" v-show="showNextButton" @click="goNextPage()">Próximo</a>
    <ul>
      <li>
        <a class="button" v-show="showPreviousButton" @click="goFirstPage()">1</a>
      </li>
      <li>
        <span v-show="showPreviousButton">...</span>
      </li>
      <li>
        <a class="button" v-show="showPreviousButton" @click="goPage(page-1)">{{page-1}}</a>
      </li>
      <li>
        <span class="button is-primary">{{page}}</span>
      </li>
      <li>
        <a class="button" v-show="showNextButton" @click="goPage(page+1)">{{page+1}}</a>
      </li>
      <li>
        <span class="button" v-show="showNextButton" @click="goLastPage()">{{totalPages}}</span>
      </li>
    </ul>
  </nav>
</template>
<script>
  export default{
    props: ["total", "page", "itensPerPage"],
    computed: {
      totalPages: function(){
        return Math.ceil(this.total/this.itensPerPage)||1
      },
      showNextButton: function(){
        return this.page!=1
      }
    },
    methods: {
      goNextPage: function(){
        this.$emit('change-page', this.page+1)
      },
      goPreviousPage: function(){
        this.$emit('change-page', this.page-1)
      },
      goFirstPage: function(){
        this.$emit('change-page', 1)
      },
      goLastPage: function(){
        this.$emit('change-page', this.totalPages)
      },
      goPage: function(page){
        this.$emit('change-page', page)
      }
    }
  }
</script>
