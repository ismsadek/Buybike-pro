<template>
	<div class="container mt-4">
		<div class="row">
		<h4>The motorbikes that we have found based on your preferences are the following: </h4><br>
		</div>
		<div class="row">
			<div class="col-6">
				<div>
				  <b-dropdown id="ddown1" text="Sort By" class="m-md-2">
				    <!-- <b-dropdown-item @click="sortBikesByBrand">Brand</b-dropdown-item> -->
				    <b-dropdown-item @click="sortBikesByPrice">Lowest price</b-dropdown-item>
				    <b-dropdown-item @click="sortBikesByPower">Minimum power</b-dropdown-item>
				  
				  </b-dropdown>
				</div>
			</div>
			<div class="col-6">
				<router-link :to="{name:'homeLink'}">
					<b-btn class="mt-4" v-b-popover.hover.focus="'Clear everything!'" variant="outline-danger"@click="clearUsersDb" id="clear"> Clear </b-btn><br><br>
				</router-link>
			</div>
			</div>
		

		<div id="bikes" class="container back mt-5 ">
			<div class="row">
			<div class="card-group pt-2 pb-2 col-sm-3 col-md-4" v-for="moto in final">
				<div class="card m-2">
					<img v-bind:src="moto.foto" alt="imagen de la moto" class="img fluid card-img-top">
			 		<div class="card-body"> 
				 		<ul class="card-text">
							<li>Brand: <strong>{{moto.marca}}</strong> </li>
							<li>Model: <strong>{{moto.modelo}}</strong></li> 
							<li>Maximum Power: {{moto.potencia}}cv</li>
							<li>Displacement: {{moto.cilindrada}}cc</li>  
							<li>Price: <strong>{{moto.precio}}</strong> €</li>
						</ul>
					</div>
				</div>
			</div>
			</div>
		</div>

		<div v-if="sortBikesByPrice" >
			<div id="price" class="container back mt-5 ">
				<div class="row">
				<div class="card-group pt-2 pb-2 col-sm-3 col-md-4" v-for="moto in sortedPrice">
					<div class="card m-2">
						<img v-bind:src="moto.foto" alt="imagen de la moto" class="img fluid card-img-top">
						<div class="card-body"> 
							<ul class="card-text">
								<li>Brand: <strong>{{moto.marca}}</strong> </li>
								<li>Model: <strong>{{moto.modelo}}</strong></li> 
								<li>Maximum Power: {{moto.potencia}}cv</li>
								<li>Displacement: {{moto.cilindrada}}cc</li>  
								<li>Price: <strong>{{moto.precio}}</strong> €</li>
							</ul>
						</div>
					</div>
				</div>
				</div>
			</div>
		</div>

		<div v-if="sortBikesByPower" >
			<div id="power" class="container back mt-5 ">
				<div class="row">
				<div class="card-group pt-2 pb-2 col-sm-3 col-md-4" v-for="moto in sortedPower">
					<div class="card m-2">
						<img v-bind:src="moto.foto" alt="imagen de la moto" class="img fluid card-img-top">
						<div class="card-body"> 
							<ul class="card-text">
								<li>Brand: <strong>{{moto.marca}}</strong> </li>
								<li>Model: <strong>{{moto.modelo}}</strong></li> 
								<li>Maximum Power: {{moto.potencia}}cv</li>
								<li>Displacement: {{moto.cilindrada}}cc</li>  
								<li>Price: <strong>{{moto.precio}}</strong> €</li>
							</ul>
						</div>
					</div>
				</div>
				</div>
			</div>
		</div>
			

		<div class="container text-center">
			<iframe src="https://www.google.com/maps/embed?pb=!1m16!1m12!1m3!1d51187.052483720814!2d-4.470201653592519!3d36.69395318124713!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!2m1!1sconcesionarios+motos+malaga!5e0!3m2!1ses!2ses!4v1527147770149" width="600" height="450" frameborder="0" style="border:0" allowfullscreen></iframe>
		</div>
	</div>
</template>

<script>
	import { dbMotosRef } from '../firebase'
	import { dbUsersRef } from '../firebase'
	import { dbFilterOneRef } from '../firebase';
	import { dbFilterTwoRef } from '../firebase';
	import { dbFilterThreeRef } from '../firebase';	
	import { dbFinalRef } from '../firebase'
	import { dbBrandRef } from '../firebase'
	import { dbSortedByPrice } from '../firebase'
	import { dbSortedByPower } from '../firebase'
	import axios from 'axios';

	import { db } from '../firebase';

	export default {
		data(){
			return{
				motos: [],
				users: [],
				errors: [],
				sortable: [],
				power: []
			}
		},
		methods : {
			clearUsersDb(){
				dbUsersRef.remove();
				dbFilterOneRef.remove();
				dbFilterTwoRef.remove();
				dbFilterThreeRef.remove();
				dbFinalRef.remove();
				dbSortedByPrice.remove();
				dbSortedByPower.remove();
				
			},

			sortBikesByPrice(){
				// Initial clear of the db
				dbSortedByPrice.remove();

				document.getElementById('bikes').style.display = "none";
				document.getElementById('power').style.display = "none";
				document.getElementById('price').style.display = "flex";
				
				let sortable = [];
				//Pushing the bikes into a new array
				for(let moto in this.motos){
					sortable.push(this.motos[moto])
				}
				// Sorting bikes from the lowest price to the highest
				sortable.sort((a, b) => a.precio - b.precio);
				// Pushing the sorted bikes into the db
				for(let moto in sortable){
					dbSortedByPrice.push(sortable[moto]) 
				}		
			},
			sortBikesByPower(){
				// Initial clear of the db
				dbSortedByPower.remove();

				document.getElementById('bikes').style.display = "none";
				document.getElementById('price').style.display = "none";
				document.getElementById('power').style.display = "flex";
				let power = [];
				//Pushing the bikes into a new array
				for(let moto in this.motos){
					power.push(this.motos[moto])
				}
				power.sort((a, b) => parseFloat(a.potencia) - parseFloat(b.potencia));
				
				for(let moto in power){
					dbSortedByPower.push(power[moto]) 
				}	
			},
			// sortBikesByBrand(){

			// }
		},
		
		created() {
			// Calling Firebase with axios request
	  	axios.get(`https://buy-bike.firebaseio.com/final.json`)
	    	.then(response => {
	      	// JSON responses are automatically parsed.
	      	this.motos = response.data
	      })
		    .catch(e => {
		      this.errors.push(e)
		    })
			    
		},

			
		firebase: {
			motos: {
				source: dbMotosRef
			},
			users: {
				source: dbUsersRef
			},
			filter1:{
				source: dbFilterOneRef
			},
			filter2:{
				source: dbFilterTwoRef
			},
			filter3:{
				source: dbFilterThreeRef
			},
			final:{
				source: dbFinalRef
			},
			sortedPrice:{
				source: dbSortedByPrice
			},
			sortedPower: {
				source: dbSortedByPower
			}
		}
	}
	
		
	
</script>

<style>
	
	#clear {
		float: right;

	}
	.back {
		/*background-color: #BDBDBD;*/
		margin-bottom: 15px;

	}
	.card-img-top{
		height: 250px;
		
	}
	
	h4 {
    font-family: 'Raleway', sans-serif;
  }


</style>
