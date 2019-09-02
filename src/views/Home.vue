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

						></v-text-field>
						</div>
						<v-btn @click="buscar_p" pa-3  medium  color="success">Consultar</v-btn>
					</v-flex>
			
			<!-- cards -->
			
					<v-layout row wrap>
						
						
							<tarjeta xs4 d-flex md4 pa-4 xs6 v-for="item in personajes" :key="item.id" :item="item" />
						
					</v-layout>
				
			</v-layout>

		</v-layout>

		<!-- paginacion -->
		
		<v-layout row wrap justify-center my-4>
			<v-flex xs4 d-flex justify-space-around align-center>
				<v-btn  
					text small 
					color="primary" @click="changePage(page -  1)"
				
					>
					atras
				</v-btn>
				<v-btn rounded text color="primary" dark>{{page}}/{{pages}}</v-btn>
				
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
	import Tarjeta from'../components/Tarjeta'

	export default {
		components: {
			Tarjeta,
		},
		data() {
			return {
				name:'',
				link: "",
				personajes: [],
				page:1,
				pages: 1,
				cantidad: 5,
				config_axios:{}
			}
		},
		
		mounted (){
			console.log('mounted active')
			this.define_configAxios();
			
		},

		methods:{
			define_configAxios(){
				const config_axios = {
					url:'https://rickandmortyapi.com/api/character/',
					method: 'get',
					responseType: 'json',
					data:{},
					header:{
						'Content-Type': 'application/json'
					},
					params:{
						name : this.name,
						page : this.page,
						pages : this.cantidad,
					}
				};
				this.config_axios = config_axios;
				console.log("se esta redefiniendo la configuracion de axios")

			},

			buscar_p(){
				this.define_configAxios();
				console.log(this.config_axios);
				console.log("coño de la madre nojoda");

				axios.request(this.config_axios).then((response) => {
					console.log("datos traidos: " + response)
					console.log('llamando datos!')
				})
			}


			// 	dameDatos(){
			// 		const params = {
			// 			page: this.page,
			// 			name: this.name
			// 		};
			// 		let result = axios
			// 			.get("https://rickandmortyapi.com/api/character/", {params})
			// 			.then(res =>{
			// 				this.pages = res.data.info.pages;
			// 				this.personajes = res.data.results
			// 				console.log(res)
			// 			})
			// 		console.log("llamado a datos!")
			// 	},

			// 	changePage(page){
			// 		this.page = page <=0 || page > this.pages ? this.page : page;
			// 		this.dameDatos();
			// 		console.log(page)
			// 	},
			// 	buscar(){
			// 		this.page = 1
			// 		this.dameDatos()
			// 		console.log("buscando a " + this.name)
			// 	}
		},
	}
</script>


<style lang="stylus" scoped>
.formName
	margin 15px 20px

</style>
