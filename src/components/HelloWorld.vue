<template>
  <div id="hello">
    <div class="text-uppercase text-bold">id selected: {{ selected }}</div>
    <table class="table table-striped table-hover">
      <thead>
        <tr>
          <th>modal</th>
          <th>id</th>
          <th>name</th>
          <th>email</th>
          <th>
            <label for="sim">Sim</label>
            <input
              type="radio"
              id="sim"
              v-model="selecao_global"
              :value="true"
              name="aprovar_reprovar"
            />
            <label for="nao">Não</label>
            <input
              type="radio"
              id="nao"
              v-model="selecao_global"
              :value="false"
              name="aprovar_reprovar"
            />
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="i in items" :key="i.id">
          <td>
            <button @click="abrirModal(i)">Editar</button>
          </td>
          <td>{{ i.id }}</td>
          <td>{{ i.name }}</td>
          <td>{{ i.email }}</td>
          <td>
            <label class="form-checkbox">
              <label for="sim">Sim</label>
              <input
                type="radio"
                :id="'sim_' + i.id"
                :value="true"
                v-model="i.aprovado"
                :name="'ar_' + i.id"
              />
              <label for="sim">Não</label>
              <input
                type="radio"
                :id="'nao_' + i.id"
                :value="false"
                v-model="i.aprovado"
                :name="'ar_' + i.id"
              />
              <i class="form-icon"></i>
            </label>
          </td>
        </tr>
      </tbody>
    </table>

    <modal :show="mostrarModal" :titulo="tituloModal" @fechar="fecharModal">
      <form>
        <label for="id">id:</label>
        <input type="text" id="id" v-model="item.id" />

        <label for="nome">Nome:</label>
        <input type="text" id="nome" v-model="item.name" />

        <label for="email">Email:</label>
        <input type="email" id="email" v-model="item.email" />

        <button type="button" @click="salvar">Salvar</button>
      </form>
    </modal>
  </div>
</template>

<script>
import Modal from "./Modal.vue";

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  components: {
    Modal,
  },
  data() {
    return {
      items: [
        {
          id: 1,
          name: "Pessoa 1",
          email: "um@example.com",
          aprovado: false,
        },
        {
          id: 2,
          name: "Pessoa 2",
          email: "dois@example.com",
          aprovado: false,
        },
      ],
      selecao_global: null,
      selected: [],
      mostrarModal: false,
      tituloModal: "Teste modal",
    };
  },
  watch: {
    selecao_global: function (valor) {
      console.log(valor);
      this.selected = [];
      for (var i = 0; i < this.items.length; i++) {
        this.items[i].aprovado = valor;
        this.selected.push(this.items[i].id);
      }
    },
  },
  methods: {
    abrirModal(item) {
      this.item = { ...item };
      this.tituloModal = "Editar pessoa";
      this.mostrarModal = true;
    },
    fecharModal() {
      this.mostrarModal = false;
    },
    salvar() {
      this.items = this.buscarItems();
      this.fecharModal();
    },
    buscarItems() {
      // lógica para buscar a lista de pessoas atualizada
      // ...

      return [
        { id: 1, nome: "João", email: "joao@example.com", aprovado: true },
        { id: 2, nome: "Maria", email: "maria@example.com", aprovado: true },
        { id: 3, nome: "José", email: "jose@example.com", aprovado: true },
        { id: 4, nome: "Pedro", email: "pedro@example.com", aprovado: true },
      ];
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
