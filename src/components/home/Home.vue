<template>
  <div>

    <h1 class="titulo">{{ titulo }}</h1>

    <input class="filtro" type="search" placeholder="Nome da imagem" v-on:input="filtrar($event)">

    <ul class="lista-fotos">
      <li class="lista-fotos-item" v-for="foto of fotosFiltradas" :key="foto.titulo">

        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva :url="foto.url" :titulo="foto.titulo"></imagem-responsiva>
        </meu-painel>
      </li>
    </ul>

  </div>
</template>

<script>
import Painel from '../shared/painel/Painel.vue';
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue';

export default {
  components: {
    'meu-painel': Painel,
    'imagem-responsiva': ImagemResponsiva
  },

  data () {
    return {
      titulo: "AluraPic",
      fotos: [],
      filtro: "",

      filtrar(evt) {
        this.filtro = evt.target.value;
      }
    }
  },

  computed: {
    fotosFiltradas() {
      if(this.filtro) {
        let regex = new RegExp(this.filtro, 'i');
        return this.fotos.filter(f => regex.test(f.titulo));
      }
      else return this.fotos;
    }
  },

  created() {
    this.$http.get("http://localhost:3000/v1/fotos")
    .then(resp => resp.json())
    .then(fotos => {this.fotos = fotos})
  },
}
</script>

<style scoped>
.titulo {
    text-align: center;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }

  .filtro {
    width: 100%;
    display: block;
  }
</style>
