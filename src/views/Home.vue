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
        <b-button variant="success" :active="active">Pesquisar</b-button>
      </b-col>
    </b-row>
    <b-row class="mt-3" v-if="!waiting">
      <b-col>
        <b-card v-if="result" :title="result.description">
          <b-card-text>
            Histórico
            <b-list-group>
              <b-list-group-item v-for="item in result.history" :key="item">
                <b-row>
                  <b-col>
                  {{item.date.format("MMM Do YYYY, h:mm:ss")}}
                  </b-col>
                  <b-col>
                    {{item.comments}}
                  </b-col>
                  <b-col>
                    {{item.city}} - {{item.state}}
                  </b-col>
                </b-row>
              </b-list-group-item>
            </b-list-group>
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

export default {
  name: 'Home',
  data: () => ({
    search: "",
    active: true,
    waiting: true,
    loading: false,
    result: {
      description: "#XPTO",
      history: [
        {
          date: moment(),
          city: "São Paulo",
          state: "SP",
          comments: "Objeto Postado"
        },
        {
          date: moment().add(1, "day"),
          city: "São Paulo",
          state: "SP",
          comments: "Objeto saiu para entrega"
        }
      ]
    }
  }),
  methods: {

  }
}
</script>
