<template>
  <div>
    <b-row>
      <b-col sm="3">
        <label>Digite o código de rastreio ou seu CPF</label>
      </b-col>
      <b-col sm="7">
        <b-input v-model="search"/>
      </b-col>
      <b-col sm="2">
        <b-button
            @click="doSearch" variant="success" :active="active">Pesquisar
        </b-button>
      </b-col>
    </b-row>
    <b-row class="mt-3" v-if="!waiting">
      <b-col>
        <b-card v-if="result" :title="result.description">
          <b-card-text>
            <div v-if="typeof result === 'object'">
              Histórico
              <b-list-group>
                <b-list-group-item v-for="item in result.history" :key="item.id">
                  <b-row>
                    <b-col>
                      {{ formatDate(item.date) }}
                    </b-col>
                    <b-col>
                      {{ item.comments }}
                    </b-col>
                    <b-col>
                      {{ item.city }} - {{ item.state }}
                    </b-col>
                  </b-row>
                </b-list-group-item>
              </b-list-group>
            </div>
            <div v-else>
              <b-table :items="result">

              </b-table>
            </div>
          </b-card-text>
        </b-card>
        <b-card v-else>
          Seu código de rastreamento não retornou resultados
        </b-card>
      </b-col>
    </b-row>
    <b-row class="mt-3" v-else-if="loading">
      <b-col class="text-center mt-3">
        <b-spinner variant="success"></b-spinner>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import moment from "moment";
import axios from "axios";

export default {
  name: 'Home',
  data() {
    return {
      search: "",
      active: true,
      waiting: true,
      loading: false,
      result: null
    }
  },
  methods: {
    doSearch() {
      if (this.search.length) {
        this.loading = true;
        axios.get(`packages/search?q=${this.search}`).then(res => {
          this.result = res.data;
        }).finally(() => {
          this.loading = false
          this.waiting = false;
        })
      }
    },
    formatDate(date) {
      return moment(date).format("MMM Do YYYY, h:mm:ss")
    }
  }
}
</script>
