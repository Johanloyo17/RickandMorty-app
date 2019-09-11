<template>
	<v-container class="contenedor" app grid-list-xl >
		<v-layout row wrap>
			
			<v-layout row wrap justify-center>
					<v-flex xs12 d-flex justify-center my-5 align-center>
						<div class="xs4">
							<v-text-field
								v-model="name"
								label="Nombre del personaje" ma-3
								@keyup.enter="buscar_p" class="formName"
								>
							</v-text-field>
						</div>
						<!-- boton buscar -->
						<v-btn 
							@click="buscar_p" pa-1  
							medium  color="success"
							>
								Buscar
						</v-btn>
					</v-flex>
			

			<ShowMore
				:characterSelected="characterSelected"
				:IsModal="IsModal" :Isloading="IsloadingModal"
				@closeModal="IsModal=false"
			/>
			<!-- cards Galery-->
					<v-layout row wrap>
						<tarjeta class="ma-4 "
								v-for="item in personajes" 
								:key="item.id" :item="item" 
								@showModal="showModal"
						/>
					</v-layout>
			</v-layout>

		</v-layout>

		<!-- paginacion -->
		<v-layout  v-if="search" row wrap justify-center my-4>
			<v-flex xs4 d-flex justify-space-around align-center>
				<!-- boton -1 -->
				<v-btn  
					text small 
					color="primary" @click="changePage(page -  1)"
					>
					atras
				</v-btn>

				<v-btn rounded text color="primary" dark>{{page}}/{{pages}}</v-btn>
				<!-- boton +1 -->
				<v-btn  
					text small 
					color="primary" @click="changePage(page + 1)"
					>
					Sigiente
				</v-btn>
			</v-flex>
		</v-layout>

	</v-container>
</template>

<script>
	import axios from "axios";
	import Tarjeta from'../components/Tarjeta';
	import ShowMore from'../components/ShowMore'
	import { async } from 'q';

	export default {
		components: {
			Tarjeta,
			ShowMore
		},
		data() {
			return {
				name:'',
				link: "",
				config_axios:{},
				//info search Characters
				personajes: [],
				page:1,
				pages: 1,
				
				search: false,

				// if search one character
				characterSelected:{},
				IsModal:false,
				//loader one character
				IsloadingModal: false, 
			}
		},
		
		mounted (){
			console.log('mounted active')
			this.define_configAxios();
			
		},

		methods:{
			// metodo para definir la configuracion axios 
			define_configAxios(){
				const config_axios = {
					url:'https://rickandmortyapi.com/api/character/',
					method: 'get',
					header:{
						'Content-Type': 'application/json'
					},
					params:{
						name : this.name,
						page : this.page,
						
					}
				};
				this.config_axios = config_axios;
				console.log("se esta redefiniendo la configuracion de axios")
			},

			//metodo para buscar personajes por nombre PRIMARY
			buscar_p(){
				this.define_configAxios();
				console.log(this.config_axios);
				console.log(" iniciando busqueda de personaje");

				axios.request(this.config_axios)
					.then((response) => {
						console.log('llamando datos!');
						console.log(response);
						this.personajes = response.data.results;
						this.pages = response.data.info.pages;
						this.search= true; 
					})
			},

			//magination method
			changePage(page){
					this.page = page <=0 || page > this.pages ? this.page : page;
					this.buscar_p();
					console.log(page)
			},
			//metodo que recibe de showmore para enviar la id y realizar un busqueda de un personaje escogido
			showModal(id){
				console.log("personaje de ID: " + id);
				this.fechPersonaje(id);
				this.IsloadingModal = true;
			},

			//metodo para buscar un personaje en especifico 
			async fechPersonaje(id) {
				let params = id
				let result = await axios.get(this.config_axios.url+params)
				this.characterSelected = result.data;
				console.log(result);
				this.IsloadingModal = false
				this.IsModal = true
				
			},

		},
	}
</script>


<style lang="stylus" scoped>
.formName
	margin 15px 20px

</style>
