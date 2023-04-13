<template>
  <div>
    <h1>Lista de clientes</h1>
    <table>
      <thead>
        <tr>
          <th>Nome</th>
          <th>Data e Hora de Entrada</th>
          <th>QRCode</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(cliente, index) in clientes" :key="cliente.id">
          <td>{{ cliente.nome }}</td>
          <td>{{ cliente.dataEntrada }} {{ cliente.horaEntrada }}</td>
          <td v-html="getQRCode(cliente.paginaAleatoria)"></td>
          <td>
            <button @click="editarCliente(index)">Editar</button>
            <button @click="excluirCliente(index)">Excluir</button>
          </td>
        </tr>
      </tbody>
    </table>
    <form v-if="exibirFormulario">
      <label for="nome">Nome:</label>
      <input type="text" id="nome" v-model="novoCliente.nome" required />
      <label for="dataEntrada">Data:</label>
      <input
        type="date"
        id="dataEntrada"
        v-model="novoCliente.dataEntrada"
        required
      />
      <label for="horaEntrada">Hora:</label>
      <input
        type="time"
        id="horaEntrada"
        v-model="novoCliente.horaEntrada"
        required
      />
      <label for="paginaAleatoria">Página Aleatória:</label>
      <input
        type="text"
        id="paginaAleatoria"
        v-model="novoCliente.paginaAleatoria"
        required
      />
      <button type="submit" @click.prevent="adicionarCliente">Adicionar</button>
      <button @click.prevent="cancelarFormulario">Cancelar</button>
    </form>
    <button @click="exibirFormulario = true">Novo Cliente</button>
  </div>
</template>
<script>
import QRCode from "qrcode-generator";

export default {
  data() {
    return {
      clientes: [
        {
          id: 1,
          nome: "João Silva",
          dataEntrada: "2022-01-01",
          horaEntrada: "08:00",
          paginaAleatoria: "https://www.exemplo.com/pagina1",
        },
        {
          id: 2,
          nome: "Maria Souza",
          dataEntrada: "2022-01-02",
          horaEntrada: "09:00",
          paginaAleatoria: "https://www.exemplo.com/pagina2",
        },
        {
          id: 3,
          nome: "Pedro Costa",
          dataEntrada: "2022-01-03",
          horaEntrada: "10:00",
          paginaAleatoria: "https://www.exemplo.com/pagina3",
        },
      ],
      exibirFormulario: false,
      novoCliente: {
        nome: "",
        dataEntrada: "",
        horaEntrada: "",
        paginaAleatoria: "",
      },
    };
  },
  methods: {
    getQRCode(link) {
      const qr = QRCode(0, "L");
      qr.addData(link);
      qr.make();
      return qr.createImgTag(4);
    },
    adicionarCliente() {
      const novoId = this.clientes.length + 1;
      const { nome, dataEntrada, horaEntrada, paginaAleatoria } =
        this.novoCliente;
      const novoCliente = {
        id: novoId,
        nome,
        dataEntrada,
        horaEntrada,
        paginaAleatoria,
      };
      this.clientes.push(novoCliente);
      this.novoCliente = {
        nome: "",
        dataEntrada: "",
        horaEntrada: "",
        paginaAleatoria: "",
      };
      this.exibirFormulario = false;
    },
    editarCliente(index) {
      const cliente = this.clientes[index];
      this.novoCliente = {
        nome: cliente.nome,
        dataEntrada: cliente.dataEntrada,
        horaEntrada: cliente.horaEntrada,
        paginaAleatoria: cliente.paginaAleatoria,
      };
      this.clientes.splice(index, 1);
      this.exibirFormulario = true;
    },
    excluirCliente(index) {
      this.clientes.splice(index, 1);
    },
    cancelarFormulario() {
      this.novoCliente = {
        nome: "",
        dataEntrada: "",
        horaEntrada: "",
        paginaAleatoria: "",
      };
      this.exibirFormulario = false;
    },
  },
};
</script>

<style>
table,
th,
td {
  border: 1px solid black;
  border-collapse: collapse;
}
th,
td {
  padding: 10px;
}
th {
  background-color: #ddd;
}
</style> 