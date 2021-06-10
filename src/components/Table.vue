<template>
  <table class="table">
    <thead>
    <th>Nome</th>
    <th>Email</th>
    <th>Telefone</th>
    <th>Tipo de documento</th>
    <th>Documento</th>
    <th></th>
    </thead>
    <tbody>
    <tr>
      <td>{{ fullName }}</td>
      <td>{{ pessoa.email }}</td>
      <td>{{ pessoa.phone }}</td>
      <td>{{ pessoa.typeDoc }}</td>
      <td>{{ pessoa.docNumber }}</td>
      <td>
        <button @click="$emit('change',pessoa)" class="btn btn-info">
            Editar
        </button>
        <button @click="$emit('delete',pessoa)" class="btn btn-danger">
          Remover
        </button>
      </td>
    </tr>
    </tbody>
  </table>
</template>

<script>
export default{
  props:{
    pessoa: {type: Object, required: true},
  },
  computed:{
    fullName: {
      get: function () {
        return this.pessoa.name + ' ' + this.pessoa.surname
      },
      set: function(){

      }
    }
  }
}
</script>