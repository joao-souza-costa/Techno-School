<template>
  <div>
    <transition>
      <div v-if="api" class="conteudo">
        <div>
          <h1>{{ api.nome }}</h1>
          <p>
            {{ api.descricao }}
          </p>
          <h2>Aulas</h2>
          <ul class="aulas">
            <li v-for="aula in api.aulas" :key="aula.id">
              <router-link
              :to="{name:'aula',params:{aula: aula.id}}">
                {{ aula.nome }}
              </router-link>
            </li>
          </ul>
        </div>
        <router-view></router-view>
      </div>
    </transition>
    <div v-if="loading">
      <page-loading></page-loading>
    </div>
  </div>
</template>

<script>
/* eslint-disable quotes */
// eslint-disable-next-line import/extensions
import fetchData from "@/mixins/fetchData.js";
import PageLoading from "../components/PageLoading.vue";

export default {
  components: { PageLoading },
  name: "curso",
  props: ["curso"],
  mixins: [fetchData],
  created() {
    this.fetchData(`/curso/${this.curso}`);
  },
};
</script>

<style>
.aulas li a{
  display: block;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.1);
  background-color: white;
  padding: 20px;
  margin-bottom: 10px;
  border-radius: 4px;
}

.aulas li a.router-link-active{
  background-color: #4b8;
  color: white;
}
</style>
