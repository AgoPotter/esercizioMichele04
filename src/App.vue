<script setup>

</script>

<template>
<body>
  <div class="container">
    <h1>Aggiungi Informazioni</h1>
    <div class="input-container">
      <input type="number" placeholder="Importo" id="importo" />
      <input type="text" placeholder="Causale" id="causale" />
      <button onclick="aggiungiRiga()">Aggiungi</button>
    </div>
    <div class="table-container">
      <table id="strumenti-table">
        <thead>
          <tr>
            <th class="pulsante causale" onclick="ordinaPerCausale()">Causale</th>
            <th class="pulsante importo" onclick="ordinaPerImporto()">Importo</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <!-- Le righe della tabella verranno generate dinamicamente in Vue.js -->
        </tbody>
      </table>
    </div>
    <div class="total-container">
      <p>Totale: <span id="totale">0</span></p>
      <button onclick="cancellaTabella()">Cancella Tabella</button>
    </div>
  </div>

  <script src="vue.js"></script> <!-- Assicurati di includere Vue.js nel tuo progetto -->
  <script src="script.js"></script> <!-- Il tuo file JavaScript -->
</body>
</template>

<style scoped>
body {
  background-color: antiquewhite;
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 800px;
  margin: 20px auto;
  background-color: #fff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

h1 {
  font-size: 36px;
  text-align: center;
}

.input-container {
  display: flex;
  gap: 10px;
  align-items: center;
  margin-bottom: 20px;
}

.input-container input {
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  width: 150px;
}

.input-container button {
  padding: 10px 20px;
  background-color: #007BFF;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.table-container {
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  padding: 10px;
  text-align: left;
  border-bottom: 1px solid #ccc;
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
  background-color: #009BFF;
}

th.pulsante.causale:hover,
.pulsante.causale:hover {
  background-color: #005BFF;
}

tr:hover {
  background-color: rgba(0, 0, 0, 0.1);
}

.total-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 20px;
}

.total-container button {
  background-color: #FF0000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

.total-container button:hover {
  background-color: #FF2222;
}
</style>
