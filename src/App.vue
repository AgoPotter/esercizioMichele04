<script>
export default {
  data() {
    return {
      importoDigitato: 0,
      quantitaSelezionata: 1,
      causaleDigitata: "",
        nuovoJSON:[]
          // [{
          //   importo: 0,
          //   quantita: 0,
          //   causale:"",
          // }], 
    }
  },

  methods: {
    aggiungiJSON() {
      // if (this.importoDigitato !=='' && this.quantitaSelezionata !=='' && this.causaleDigitata !=='') {
      if (this.importoDigitato !==0 && this.causaleDigitata !=='') {

        this.nuovoJSON.push({
          importo: this.importoDigitato,
          quantita: this.quantitaSelezionata,
          causale: this.causaleDigitata,        
        });
        // this.importoDigitato='';
        // this.quantitaSelezionata='';
        this.importoDigitato=0;
        this.quantitaSelezionata=1;
        this.causaleDigitata='';
        } else {

        alert("Oh oh... sembra che tu abbia dimenticato di completare tutti i campi.");
      }
    },
    rimuoviRiga(index) {
      this.nuovoJSON.splice(index, 1);
      // this.nuovoJSON.splice(this.index, 1);
    },
    cancellaTabella() {
      this.nuovoJSON=[]
    },
    ordineImporto() {
      this.nuovoJSON.sort((a, b) => a.importo - b.importo);
      /*
      Se invece volessi ordinare numericamente un array e non un JSON:
      nomeArray.sort((a, b) => a - b);
      */
    },
    ordineImportoDEC() {
      this.nuovoJSON.sort((a, b) => b.importo - a.importo);
    },
    ordineQuantita() {
      this.nuovoJSON.sort((a, b) => a.quantita - b.quantita);
    },
    ordineQuantitaDEC() {
      this.nuovoJSON.sort((a, b) => b.quantita - a.quantita);
    },
    ordineCausale() {
            /*
      Se invece volessi ordinare alfabeticamente un array e non un JSON:
      nomeArray.sort();
      Se lo volessi ordinare in modo decrescente:
      nomeArray.sort((a, b) => b.localeCompare(a));
      */
      this.nuovoJSON.sort((a, b) => a.causale.localeCompare(b.causale));
    },
    ordineCausaleDEC () {
      this.nuovoJSON.sort((a, b) => b.causale.localeCompare(a.causale));
    }
  },

  computed: {
    totaleImporti() {
      /* 
    ACC (accumulatore): Questo parametro rappresenta il valore accumulato durante 
    le iterazioni dell'array. 
    Nella prima iterazione, il valore dell'accumulatore è il valore iniziale 
    specificato come secondo argomento di reduce (nel nostro caso, 0). 
    Durante le iterazioni successive, l'accumulatore conterrà il valore accumulato finora.
    REDUCE: reduce è un metodo degli array di JavaScript che viene utilizzato 
    per eseguire una riduzione di tutti gli elementi dell'array in un singolo valore, 
    come ad esempio calcolare una somma o ottenere un valore massimo.

item: Questo parametro rappresenta l'elemento corrente dell'array su cui reduce sta iterando. Durante ogni iterazione, la funzione callback viene chiamata con l'elemento corrente e può accedere alle proprietà di quest'ultimo (nel nostro caso, accediamo alla proprietà importo dell'oggetto item).
      */
      return this.nuovoJSON.reduce((acc, item) => acc + item.importo, 0);
      /*
        return this.nuovoJSON.reduce(function(acc, item) {
        return acc + item.importo;
      }, 0);
      */
     /*
     Se volessi calcolare la somma di un array e non di un JSON, la sintassi è questa:
     const somma = nomeArray.reduce((acc, numero) => acc + numero, 0);
      */
    }
 },
}
</script>

<template>
<body>
  <div class="container">
    <header>    <h1>📯 🎷 🎺 Music Shop 🎙️ 🎸 🥁</h1>
    <h2>〽️ Gestione contabilità 〽️</h2>
    </header>
    <br>
    <div class="input-container">
      <input v-model="importoDigitato" type="number" placeholder="Importo" id="importo" />
      <select v-model="quantitaSelezionata" type="number" id="quantita" name="quantita">
          <option value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
          <option value="4">4</option>
          <option value="5">5</option>
      </select>
      <input v-model="causaleDigitata" type="text" placeholder="Causale" id="causale" />
      <button @click="aggiungiJSON()" id="aggiungi">Aggiungi</button>
    </div>
    <div class="table-container">
      <table id="strumenti-table">
        <thead>
          <tr>
            <th class="importo" @click="ordinaPerImporto()">Importo</th>
            <th class="quantita" @click="ordinaPerQuantita()">Quantita</th>
            <th class="causale" @click="ordinaPerCausale()">Causale</th> 
            <th></th>
          </tr>
          <tr v-if="nuovoJSON.length > 0">
            <th class="frecce">
              <div @click="ordineImporto">🔽</div>
              <div @click="ordineImportoDEC">🔼</div>
            </th>
            <th class="frecce">
              <div @click="ordineQuantita">🔽</div>
              <div @click="ordineQuantitaDEC">🔼</div>
            </th>
            <th class="frecce">
              <div @click="ordineCausale">🔽</div>
              <div @click="ordineCausaleDEC">🔼</div>
            </th>
            <th>
            </th></tr>
        </thead>
        <tbody v-if="nuovoJSON.length > 0">
          <tr v-for="(item, index) in nuovoJSON" :key="index">
          <td>{{ item.importo }}</td>
          <td>{{ item.quantita }}</td>
          <td>{{ item.causale }}</td>
          <td>
            <button @click="rimuoviRiga(index)">❌</button>
          </td>
        </tr>
        </tbody>
      </table>
    </div>
    <div class="total-container">
      <p id="totale">Totale: <b>{{ totaleImporti }}</b></p>
      <button @click="cancellaTabella()" id="cancella">🗑️ tabella</button>
    </div>
  </div>
  <footer><a href="https://it.freepik.com/vettori-gratuito/illustrazione-del-negozio-di-musica_3910275.htm#query=negozio%20musica%20disegno&position=28&from_view=search&track=ais">Immagine di macrovector</a> su Freepik</footer>
</body>
</template>

<style scoped>
body {
  background-color: rgba(245, 242, 242, 0.5);
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-image: url('sfondo.jpg');
  background-size: cover; /* Per adattare l'immagine allo schermo */
  background-position: center; /* Posiziona l'immagine al centro dello schermo */
  height: 100vh; /* Altezza pari all'intera finestra del browser */
}

.container {
  background-color: rgba(245, 242, 242, 0.3);
  border-radius: 30px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.7);
  width: 100%; /* Larghezza pari all'intera finestra del browser */
  height: 100vh; /* Altezza pari all'intera finestra del browser */
  padding: 60px; /* Aggiungi padding di 20px ai bordi interni del contenitore */
  box-sizing: border-box; /* Assicurati che il padding sia incluso nelle dimensioni del contenitore */

}

h1 {
  font-size: 50px;
  text-align: center;
  color:#1091e7;
  text-shadow: 2px 2px 5px rgba(200, 200, 200, 0.5);
}

h2 {
  font-size: 35px;
  text-align: center;
  color:#dce710;
  text-shadow: 2px 2px 5px rgba(200, 200, 200, 0.5);
}

#totale {
  font-size: 30px;
  color: whitesmoke;
}

footer, header {
  background-color: #030837de; /* Sfondo blu scuro */
  color: #fff; /* Testo bianco */
  text-align: center; /* Centra il testo */
  padding: 20px; /* Aggiunge spazio interno al footer */
  border-radius: 10px; /* Bordi arrotondati */
}


.input-container {
  display: flex;
  gap: 10px;
  align-items: center;
  margin-bottom: 20px;
}

.input-container input {
  border: 1px solid #ccc;
  font-size: 24px; /* Imposta la dimensione del testo a 24px */
  font-family: 'Nunito', sans-serif; /* Utilizza il font 'Nunito' come esempio (assicurati di averlo importato nell'HTML) */
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  width: 150px;
}

#aggiungi {
  width: 150px;
  height: 50px;
  font-size: 24px;
  background-color: #0a8a0e;
   color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

#aggiungi:hover {
  background-color: #009BFF;
  color: #fff; /* Puoi anche cambiare il colore del testo all'hover se lo desideri */
}

#cancella {
  width: 240px;
  height: 50px;
  font-size: 24px;
}
.input-container button {
  padding: 10px 20px;
  background-color: #059a2a;
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

.total-container {
  display: flex;
  background-color: #030837de;
  color: antiquewhite;
  justify-content: space-between;
  align-items: center;
  margin-top: 10px;
  border-radius: 10px;
  padding: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 20px;
}
.total-container p {
  transform: translateX(20px); /* Sposta il paragrafo di 20px verso sinistra (verso il centro) */
}

.total-container button {
  transform: translateX(-20px); /* Sposta il pulsante di 20px verso destra (verso il centro) */
}

.total-container button {
  background-color: #760505;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

.total-container button:hover {
  background-color: rgba(255, 34, 34, 0.586);
}

.input-container input {
  font-size: 24px;
  font-family: 'Nunito', sans-serif;
  padding: 10px;
  border: 2px solid #222; /* Aggiunge un bordo nero spesso di 2px */
  border-radius: 5px;
}

.input-container input, 
.input-container button {
  font-size: 24px;
  font-family: 'Nunito', sans-serif;
  padding: 10px;
  border: 2px solid #222; /* Aggiunge un bordo nero spesso di 2px */
  border-radius: 5px;
}

.input-container #causale {
  width: 450px; /* Imposta il doppio della larghezza rispetto agli altri input */
}
.input-container #importo {
  width: 250px; /* Imposta il doppio della larghezza rispetto agli altri input */
}
.input-container #quantita {
  width: 80px; /* Imposta il doppio della larghezza rispetto agli altri input */
  font-size: 24px;
  font-family: 'Nunito', sans-serif;
  padding: 10px;
  border: 2px solid #222; /* Aggiunge un bordo nero spesso di 2px */
  border-radius: 5px;
  height: 50px;
}
.frecce {
    display: column;
    justify-content: center;
  }
</style>
