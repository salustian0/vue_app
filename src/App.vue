<template>
  <div id="app">
    <div class="row justify-content-center">
      <div class="col-md-8">
        <div class="card">
          <div class="card-header">Registro</div>

          <div class="card-body">
            <form v-on:submit.prevent="formAction(pessoa)">
            <div class="row">
              <div class="form-group col-6">
                <label for="name">Nome:</label>
                <input v-model="pessoa.name" id="name" class="form-control" type="text" name="name" placeholder="Seu nome">
              </div>
              <div class="form-group col-6">
                <label for="surname">Sobrenome:</label>
                <input v-model="pessoa.surname" id="surname" class="form-control" type="text" name="surname" value="" placeholder="Sobrenome">
              </div>
            </div>
            <div class="row">
              <div class="form-group col-6">
                <label for="email">Email:</label>
                <input v-model="pessoa.email" id="email" class="form-control" type="text" name="surname" value="" placeholder="Seu email ex: teste@teste.com">
              </div>
              <div class="form-group col-6">
                <label for="docNumber">Documento:</label>
                <input v-model="pessoa.docNumber" id="docNumber" class="form-control" type="text" name="docNumber" value="" placeholder="Cpf ou Cnpj">
              </div>
            </div>

            <div class="form-group col-6">
              <label for="docNumber">Telefone:</label>
              <input v-model="pessoa.phone" id="phone" class="form-control" type="text" name="phone" value="" placeholder="Telefone">
            </div>

            <div class="form-group col-6">
              <label for="docType">Tipo de documento:</label><br>
              <label class="mr-2">CPF: <input v-model="pessoa.typeDoc" id="docType" type="radio" name="docType" value="cpf"></label>
              <label>CNPJ: <input v-model="pessoa.typeDoc" type="radio" name="docType" value="cnpj"></label>
            </div>
            <div class="d-flex justify-content-center align-items-center">
              <button v-if="this.action === 'add'" class="btn btn-info">
                Adicionar pessoa
              </button>
              <button v-if="this.action === 'change'" class="btn btn-info">
                Editar
              </button>
            </div>
          </form>

          </div>
        </div>

      </div>

      <div class="col-md-8 mt-3">
        <div class="card">
          <div class="card-header">Listagem</div>

          <div class="card-body">

          </div>
        </div>
      </div>
    </div>

    <Table v-for="(p,index) in pessoas" :key="index" :pessoa="p" @change="changePessoa" @delete="deletePessoa"/>
  </div>
</template>

<script>
import Table from './components/Table.vue'

export default {
  components:{
    Table
  },
  data(){
    return{
      pessoas:[],
      pessoa: {},
      action : 'add',
      current_index : 0
    }
  },
  name: 'App',
  methods:{
    formAction(pessoa){
      if(this.action === "add"){
        this.addPessoa(pessoa)
      }else if(this.action === "change"){
        this.savePessoa(pessoa);
      }
    },
    addPessoa(){
      this.pessoa.id = Date.now();
      let required_indexes = ['name','email','surname','typeDoc','docNumber','phone'];
       for(let key in required_indexes){
         if(this.pessoa[required_indexes[key]] === undefined){
           alert('Por favor preencha todos os campos');
           return;
         }
       }

      this.pessoas.push(this.pessoa);
      this.pessoa = {};
      alert('Item adicionado');

    },
    changePessoa(pessoa){
      //Buscando indice de acordo com o id
      const index = this.pessoas.findIndex(item => item.id === pessoa.id);
      this.current_index = index;
      for (let key in this.pessoas[index]){
        this.pessoa[key] = this.pessoas[index][key];
      }
      this.action = 'change';
    },
    savePessoa(pessoa){
      const index = this.pessoas.findIndex(item => item.id === pessoa.id);
      this.$set(this.pessoas,index,this.pessoa);
      this.pessoa = {};
      this.action = 'add';
    },
    deletePessoa(pessoa){
      const index = this.pessoas.findIndex(item => item.id === pessoa.id);
      this.$delete(this.pessoas,index);
      alert('Item deletado');
    }
  },
  watch:{
    pessoa(){

    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
