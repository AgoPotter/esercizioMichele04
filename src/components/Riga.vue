<template>
    <tr>
        <td>{{ riga.importo }}</td>
        <td>{{ riga.quantita }}</td>
        <td>{{ riga.causale }}</td>
        <td> <button @click="rimoviRigaDaEmettere(indice)">❌</button> </td>
    </tr>
</template>

<script>
export default{
    props:["riga","indice"],
    methods:{
        rimoviRigaDaEmettere(indice){
            this.$emit('rimuoviRigaEmesso', indice)
        }
    }
}
</script>

<style scoped>
th,
td {
  padding: 10px;
  text-align: left;
  font-size: 20px;
  border-bottom: 1px solid #ccc;
  background-color: #030837de;
  color: whitesmoke;
}

th {
  cursor: pointer;
}

th.pulsante:hover,
.pulsante:hover {
  background-color: #007BFF;
  color: #fff;
}

th.pulsante.importo:hover,
.pulsante.importo:hover {
  background-color: #07a211;
}

th.pulsante.causale:hover,
.pulsante.causale:hover {
  background-color: #005BFF;
}

tr:hover {
  background-color: rgba(0, 0, 0, 0.1);
}

</style>