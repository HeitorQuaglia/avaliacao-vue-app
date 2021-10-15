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
    <b-row>
      <b-col>
        <b-card :title="result.description">
          <b-card-text>
            Histórico
            <b-list-group>
              <b-list-group-item v-for="item in result.history" :key="item">
                {{item}}
              </b-list-group-item>
            </b-list-group>
          </b-card-text>
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>

<script>

export default {
  name: 'Home',
  data: () => ({
    search: "",
    active: true,
    result: {
      description: "#XPTO",
      history: [
        "XPTO"
      ]
    }
  }),
  methods: {

  }
}
</script>
