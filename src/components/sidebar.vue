<template>
    	<nav>
		<v-navigation-drawer v-model="open" class="coll">
			<!-- <v-list nav dense class="coll">
				<v-list-item-group class="px-4 mx-2">
					<v-list-item class="list-item py-5 my-5" router to="/operator">
						<v-list-item-title>
							<v-icon>mdi-file-multiple</v-icon>
							<button
								@click="retrieveFiles"
								class="ps-4 text word"
								router
								to="/files"
							>
								My Files
							</button>
						</v-list-item-title>
					</v-list-item>
					<v-list-item class="list-item pb-5 mb-5" router to="/share"   flat>
						<v-list-item-title router to="/share">
							<v-icon>mdi-send </v-icon>
							<button class="ps-4 text word" flat>Send Documents</button>
						</v-list-item-title>
					</v-list-item>
                    <v-list-item class="list-item pb-5 mb-5" router to="/sharedDocs"   flat>
						<v-list-item-title router to="/sharedDocs">
							<v-icon>mdi-inbox </v-icon>
							<button class="ps-4 text word" @click="receiveDocuments" flat>Shared Documents</button>
						</v-list-item-title>
					</v-list-item>
					<v-list-item class="list-item" router to="/verify">
						<v-list-item-title>
							<v-icon> mdi-check-decagram</v-icon>
							<button class="ps-4 text word" router to="/verify">Verify</button>
						</v-list-item-title>
					</v-list-item>
				</v-list-item-group>
			</v-list> -->

			<!-- <v-card color="white" class="cardpos mx-5 px-5">
				<v-img src="../assets/rect.svg" width="97px" class="pt-5 mt-5"></v-img>
				<p class="font-weight-light card-text-color">75% Used</p>
				<v-progress-linear class="progress" height="6"></v-progress-linear>
				<div class="unit-center pt-4 mt-3 mb-3 pb-2">
					<v-btn class="coll" flat>upgrade</v-btn>
				</div> 
			</v-card> -->
		</v-navigation-drawer>
		<v-toolbar class="coll" >
			<v-app-bar-nav-icon
				class="hidden-md-and-up"
				@click.stop="open = !open"
			></v-app-bar-nav-icon>
			<v-toolbar-title class="word">BOOKee </v-toolbar-title>

			<input placeholder="search" class="input form-control" />

			<!-- <v-btn icon>
				<v-icon>mdi-heart</v-icon>
			</v-btn> -->

			
			<v-btn color="" v-bind="attrs" v-on="on" class="">
							<v-icon>mdi-wallet</v-icon>

							<span class="" @click="connectWallet">Connect</span></v-btn
						>

	 
		</v-toolbar>
	</nav>
</template>
<script>
 	import emitter from "tiny-emitter/instance";
	// import { ConnectButton } from "web3uikit";
	import { create } from "ipfs-client";
	import { ethers, Signer } from "ethers";
	import { abi, contractAddress } from "../../constants";

export default {
    name:"navBar",
	components: {
	 
  },
    	data() {
			return {
				dialog: false,
				mem: [],
				documents: [],
				receivedDocs:[],
				open: true,
				group: null,
				file: "",
				comment: "",
				fileName: "",
				time: "",
            }
        },
		methods:{

			async connectWallet() {
				if (typeof window.ethereum !== "undefined") {
					await window.ethereum.request({ method: "eth_requestAccounts" });
					dialog =true
				}
			},


				async receiveDocs() {
                const provider = new ethers.providers.Web3Provider(window.ethereum);
				const signer = await provider.getSigner();
				const contract = new ethers.Contract(contractAddress, abi, signer);
                 const receivedDocs = await contract.receivedDocs()
                 return receivedDocs;
            },
		}
 
 }
</script>
<style scoped>
.word {
		color: #095073;
		font-size:xx-large
	}

	.coll {
		background-color:rgb(238,254,252);
	}
</style>
