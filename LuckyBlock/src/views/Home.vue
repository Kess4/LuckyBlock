<script>

import BlockR from '../assets/blockr.svg'
import BlockB from '../assets/blockb.svg'
import BlockG from '../assets/blockg.svg'
import Web3 from 'web3'

document.addEventListener('DOMContentLoaded', async () => {
    await chargerContrat();

});

let compte
let adresseContrat = '0x22C107F58dcE8cb0cff66a637F593A16dEa44c15'; // Adresse réelle du contrat
let abiContrat = [
        {
            "inputs": [],
            "name": "effectuerTirage",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
        },
        {
            "inputs": [],
            "name": "envoyerFonds",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
        },
        {
            "inputs": [],
            "name": "participer",
            "outputs": [],
            "stateMutability": "payable",
            "type": "function"
        },
        {
            "inputs": [],
            "stateMutability": "nonpayable",
            "type": "constructor"
        },
        {
            "anonymous": false,
            "inputs": [
                {
                    "indexed": false,
                    "internalType": "address",
                    "name": "gagnant",
                    "type": "address"
                }
            ],
            "name": "TirageEffectue",
            "type": "event"
        },
        {
            "inputs": [],
            "name": "gagnant",
            "outputs": [
                {
                    "internalType": "address",
                    "name": "",
                    "type": "address"
                }
            ],
            "stateMutability": "view",
            "type": "function"
        },
        {
            "inputs": [],
            "name": "montantDuTirage",
            "outputs": [
                {
                    "internalType": "uint256",
                    "name": "",
                    "type": "uint256"
                }
            ],
            "stateMutability": "view",
            "type": "function"
        },
        {
            "inputs": [],
            "name": "nombreParticipants",
            "outputs": [
                {
                    "internalType": "uint256",
                    "name": "",
                    "type": "uint256"
                }
            ],
            "stateMutability": "view",
            "type": "function"
        },
        {
            "inputs": [
                {
                    "internalType": "uint256",
                    "name": "",
                    "type": "uint256"
                }
            ],
            "name": "participants",
            "outputs": [
                {
                    "internalType": "address",
                    "name": "",
                    "type": "address"
                }
            ],
            "stateMutability": "view",
            "type": "function"
        },
        {
            "inputs": [],
            "name": "proprietaire",
            "outputs": [
                {
                    "internalType": "address",
                    "name": "",
                    "type": "address"
                }
            ],
            "stateMutability": "view",
            "type": "function"
        }
    ]; // ABI réelle du contrat

let web3 = new Web3(window.ethereum);
let contrats = new web3.eth.Contract(abiContrat, adresseContrat);

console.log("Contrat:", contrats);


 

export default {
  data() {
    return {
      items: [
        { title: 'Block 1', src: BlockG, price : "0.001 ETH"},
        { title: 'Block 2', src: BlockB, price : "0.002 ETH" },
        { title: 'Block 3', src: BlockR, price : "0.005 ETH" },
      ],
        

    };
  },

  mounted() {
    this.chargerContrat();
    this.participants();
 
  },

  methods: {

    

async chargerContrat() {
    
    // Charger le contrat
    

    const balance = await web3.eth.getBalance(adresseContrat);
    console.log("Balance du contrat:", balance);
    

    // Vérifier si le compte est connecté à MetaMask
    const comptes = await web3.eth.getAccounts();
    compte = comptes.length > 0 ? comptes[0] : null;
    if (compte === null) {
        console.error("Veuillez vous connecter à MetaMask");
    } else {
        console.log("Compte MetaMask détecté:", compte);
    }

},

async participants() {
    let parts=contrats.methods.nombreParticipants().call({ from: adresseContrat});
    console.log("Nombre de participants:", parts);
},

 async participer() {
     try {
        const participationTx = await contrats.methods.participer().send({ from: compte, value: web3.utils.toWei('0.001', 'ether') });
        console.log(participationTx);
       
     } catch (error) {
         console.error("Erreur lors de la participation:", error);
     }
},


 async effectuerTirage() {
     try {
         const tirageTx = await contrats.methods.effectuerTirage().send({ from: compte });
         console.log(tirageTx);
         
     } catch (error) {
         console.error("Erreur lors de l'effetuation du tirage:", error);
     }
 },

 async envoyerFonds() {
     try {
         const envoiFondsTx = await contrats.methods.envoyerFonds().send({ from: compte });
         console.log(envoiFondsTx);

     } catch (error) {
         console.error("Erreur lors de l'envoi des fonds:", error);
     }
 }

  },

  
};
</script>

<template>
  <v-carousel
      :continuous="false"
      :show-arrows="false"
      hide-delimiter-background
      delimiter-icon="mdi-circle"
      height="420"
      class="car"
      color="#F9E589"
    >
    
      <v-carousel-item 
        v-for="(item, i) in items"
        :key="i"
      >
        <img :src="item.src" class="car-image" /> 
          <div class="text-h6">
              {{ item.title }} -
              {{ item.price }}
          </div>
        <!-- Ajout d'une classe .car-image pour centrer les images -->
      </v-carousel-item>
  </v-carousel>




  <v-btn
    @click="participer"
      variant="flat"
      color="#5063BF"
      class="btn"
    >Participer</v-btn>
    <v-btn
    @click="effectuerTirage"
      variant="outlined"
      color="#5063BF"
      class="btn"
    >Tirage gagnant</v-btn>
    <v-btn
    @click="envoyerFonds"
      variant="outlined"
      color="#5063BF"
      class="btn"
    >Envoi Gains</v-btn>


</template>



<style scoped>
.car-image {
  display: flex;
  margin-left: auto;
  margin-right: auto;
  max-height: 300px; 
}
.infos{
  margin-top: 30px;

}
.btn{
  margin-top: 30px;
  margin-bottom: 35px;
  margin-right: auto;
  display: flex;
  margin-left: auto;
}

.text-h6 {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

</style>
