<template>
  <div id="app">
    <Bares></Bares>
    <a class="fixo button is-large is-danger is-loading" v-show="loading"> Loading</a>
    <div class="container">
      <h1 class="tittle"> {{title}} </h1>
      <div class="columns">
        <div class="column is-5">
          <p class="control has-addons">
            <input class="input is-expanded" type="text" placeholder="Procure pelo nome" v-model="search">
            <a class="button is-info" @click="serachBares">Search</a>
          </p>
        </div>
        <div class="column is-5">

        </div>
      </div>
      <div class="colums">
        <div class="colum is-12">
          <table class="table is-narrow is-bondered">
            <thead>
              <tr>
                <th>Nome</th>
                <th>Cidade</th>
                <th>Descrição</th>
                <th>Mais</th>
                <th>Ações</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="bar in bares">
                <td> {{bar.bar_ds_nome}} </td>
                <td> {{bar.bar_ds_cidade}} </td>
                <td> {{bar.bar_ds_descricao}} </td>
                <td class="is-icon">
                  <a href="#">
                    <i class="fa fa-map-marker"></i>
                  </a>
                  <a href="#">
                    <i class="fa fa-plus-circle"></i>
                  </a>
                </td>
                <td class="is-icon">
                  <a href="#">
                    <i class="fa fa-edit"></i>
                  </a>
                  <a href="#">
                    <i class="fa fa-trash"></i>
                  </a>
              </tr>
            </tbody>
          </table>
          <Paginacao :total="total" :page="page" :itens-per-page="itensPerPage" @change-page="onChangePage"></Paginacao>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Bares from './Bares.vue'
import Paginacao from './Paginacao.vue'

export default {
  data() {
    return {
      isLoading: false,
      title: 'Vuejs CRUD Bares',
      search: '',
      breweries:[],
      page: 1,
      total: 0,
      selected: {},
      itensPerPage: 10,
      bares: {}
    }
  },
  methods: {
    showLoading() {
      this.isLoading=true;
    },

    hideLoading() {
      this.isLoading=false;
    },

    loadBares(){
      let t = this;
      this.showLoading()

      let start = (this.page * this.intensPerPage) - this.itensPerPage
      let end = this.page * this.itensPerPage

      this.$http.get(`/bares`).then(
        response=>{
          this.$set('bares', response.json());
          this.$set('total', response.header['X-Total-Count']);
          console.log(bares);
        },
        error=>{
          console.log(error)
        }).finally(function () {
          t.hideLoading();
        })
    },
    searchBares() {

    }
  },
  components: {
    Bares,
    Paginacao
  }
}
</script>

<style>
body {
  margin-top:50px;
}
</style>
