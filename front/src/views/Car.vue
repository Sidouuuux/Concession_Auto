<template>
  <section class="py-20">
    <div class="container px-4 mx-auto">
      <div class="max-w-xl mx-auto text-center">
        <h2 class="mb-4 text-3xl lg:text-4xl font-bold font-heading">
          <span>Inventaire : ...</span>
          <span class="text-blue-600"> voitures</span>
        </h2>
        <p class="mb-8 text-blueGray-400">Adresse courante : {{ account }}</p>
        <p class="mb-8 text-blueGray-400">Adresse admin : {{ admin }}</p>
        <div class="flex flex-wrap max-w-lg mx-auto">
          <div
              class="flex w-full md:w-2/3 px-3 mb-3 md:mb-0 md:mr-6 bg-blueGray-100 rounded"
          >
            <textarea
                v-model="newCar"
                class="w-full pl-3 py-4 text-xs text-blueGray-400 font-semibold leading-none bg-blueGray-100 outline-none"
                type="text"
                placeholder="Nom de la voiture"
            ></textarea>
          </div>
          <button 
              v-on:click="addCar"
              class="w-full md:w-auto py-4 px-8 text-xs text-white font-semibold leading-none bg-blue-600 hover:bg-blue-700 rounded"
              type="submit">
            Enregistrer vehicule
          </button>
        </div>
      </div>
    </div>
    <section class="py-20 xl:bg-contain bg-top bg-no-repeat" style="background-image: url('metis-assets/backgrounds/intersect.svg');">
      <div class="container px-4 mx-auto">
    <h2 class="mb-4 text-3xl lg:text-4xl font-bold font-heading">
      <span class="text-blue-600">Les voitures en cours d'utilisation ...</span>
    </h2>
    <div class="p-8 bg-white shadow rounded">
            <div class="flex items-center mb-4">
              <img class="h-16 w-16 rounded-full object-cover"  alt="">
              <div class="pl-4">
                <p class="text-xl">Voiture de test</p>
              </div>
            </div>
            <br>
            <div class="flex flex-wrap max-w-lg mx-auto">
              <div
                class="flex w-full md:w-2/3 px-3 mb-3 md:mb-0 md:mr-6 bg-blueGray-100 rounded"
              >
              </div>
              <button 
                  v-on:click="participate"
                  class="bg-blue-500 rounded-lg font-bold text-white text-center px-4 py-3 transition duration-300 ease-in-out hover:bg-blue-600 mr-6"
                  type="submit"
              > Signalez une panne
              </button>
              <a v-on:click="PickWinner" class="bg-blue-500 rounded-lg font-bold text-white text-center px-4 py-3 transition duration-300 ease-in-out hover:bg-blue-600 mr-6">
                Depart vehicule
              </a>
              <a v-on:click="PickWinner" class="bg-blue-500 rounded-lg font-bold text-white text-center px-4 py-3 transition duration-300 ease-in-out hover:bg-blue-600 mr-6">
                Retour vehicule
              </a>
            </div>
          </div>
    <!-- <div >
      <RenderCar :account="account" :admin="admin" :loteryAbi="loteryAbi" :data="lotery" :loteryWin="loteriesWin"/>
    </div> -->

    <h2 class="mb-4 text-3xl lg:text-4xl font-bold font-heading">
    <span class="text-blue-600">Les voitures disponible</span>
    </h2>
    <!-- <div >
      <RenderOverCar :account="account" :admin="admin" :loteryAbi="loteryAbi" :data="lotery" :loteryWin="loteriesWin"/>
    </div> -->

    </div>
    </section>
  </section>
</template>

<script>

// import RenderLot from "@/views/components/Lotery/renderLot";
// import RenderOverLot from "@/views/components/Lotery/renderOverLot";
// import LoteryContract from '../abis/Lotery.json';
// import Web3 from 'web3';

// export default {
//   name: "Lotery",
//   components: {RenderLot, RenderOverLot},

//   data() {
//     return {
//       account: '0x0',
//       admin: '0x0',
//       currentBalance: 0,
//       loteryAbi: [],
//       loadedLoteries: [],
//       loteriesWin: [],
//       numberOfLoteries: 0,
//       loading: true,
//       isRendered: false,
//       createLoteryName : "",
//       newLotName : ""
//     };
//   },
//   async beforeMount(){
//     await this.loadWeb3();
//     await this.loadBlockchainData();
//   },
//   methods: {
    
//     async addLot(){
//       await this.loteryAbi.methods.addLotery(this.newLotName).send({ from: this.account })
//     },
//     async loadWeb3(){
//       // Setup Web3 si Metask est présent
//       if(window.ethereum){
//         window.web3 = new Web3(window.ethereum)
//         await window.ethereum.enable()
        
//         // Pas sûr de ce que ça fait j'avoue
//       } else if(window.web3){
//         window.web3 = new Web3(window.web3.currentProvider)
        
//       } else {
//         // S'affiche s'il n'y a pas de Metamask
//         window.alert('Non-Ethereum browser detected. Please download Metamask')
        
//       }
//     },
//     async loadBlockchainData(){
//       // URL Ganache
//       const web3 = new Web3(window.ethereum);
      
//       const accounts = await web3.eth.getAccounts();
//       this.account = accounts[0]
      
//       web3.eth.handleRevert = true

//       //On récupère l'ID du réseau : 5777 provenant de ganache
//       const netId = await web3.eth.net.getId()

//       // On va chercher le contrat déployé sur le réseau 5777
//       const loteryContractData = LoteryContract.networks[netId]

//       // Si on récupère quelque chose de non-vide, on créer le contrat sur web3 avec l'abi (présent dans le .json du contrat une fois compilé) et son adresse, puis on l'enregistre dans le state
//       if(loteryContractData){
//         const loteryContract = new web3.eth.Contract(LoteryContract.abi, loteryContractData.address)
//         this.loteryAbi = loteryContract
//       }else{
//         window.alert('Lotery smart contract has not been deployed to detected network')
//       }
//       try{  
        
//         // On récupère la balance de la personne connectée
//         let currentBalance = await web3.eth.getBalance(this.account);
//         currentBalance = web3.utils.fromWei(currentBalance, 'ether')
//         this.currentBalance = currentBalance

//         //On récupère combien il y a de loterie en cours
//         var res = await this.loteryAbi.methods.getLoteriesCount().call()
//         this.numberOfLoteries = res

//         /* Renvoie l'adresse de l'admin */
//         let admin = await this.loteryAbi.methods.getAdmin().call()
//         this.admin = admin

//         /* Renvoie ID + nom d'une loterie */
     

//         for (let i=0 ; i < this.numberOfLoteries; i++) {
//           var listLots = await this.loteryAbi.methods.listLoteries(i).call()
//           this.loadedLoteries.push(listLots)

//           // this.setState({loadedLoteries: this.loadedLoteries.concat(result6)})

//           var lotWin = await this.loteryAbi.methods.getLoteryGain(i).call()
//           this.loteriesWin.push(lotWin)
//           // this.setState({loteriesWin: this.loteriesWin.concat(win)})
//           // this.setState({loadedLoteries : this.loadedLoteries.push(result6)})
//         }
     
//         this.loading = false // Me permet de gérer le front tant que les données sont pas arrivées
//       }catch(e){
//         console.log("Je suis l'erreur : " + e)
//         console.log(e.message)
//       }
//     }
//   }
// };
// </script>

