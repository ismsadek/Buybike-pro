<template>

  <div class="container mt-4">
    <hr>
  	<div class="container">
     <div class="row">
       <div class="col-12">
         <h1 class="text-center font-weight-bold header">How do we work?</h1>
       </div>
     </div><hr> 
    </div>
    <div class="card-deck">
      <div class="card">
        <img class="card-img-top" src="../assets/duda.jpg" alt="dudas">
        <div class="card-body">
          <h5 class="card-title font-weight-bold">What model can I choose?</h5>
          <p class="card-text">Sometimes this part is confusing for people, because in the market there are many models and you don´t know what to choose so with our test your doubts disappear!</p>
        </div>
      </div>
      <div class="card">
        <img class="card-img-top" src="../assets/algorithm2.jpg" alt="Card image cap">
        <div class="card-body">
          <h5 class="card-title font-weight-bold">The algorithm most efficient</h5>
          <p class="card-text">Based on our technical knowledge we have created an algorithm that shows you the bikes which fits you.</p>
        </div>
      </div>
      <div class="card">
        <img class="card-img-top" src="../assets/results.png" alt="Card image cap">
        <div class="card-body">
          <h5 class="card-title font-weight-bold">Verified results</h5>
          <p class="card-text">Our clients are very proud of this app because they recognize that with this process they get a clearer idea of the models available for them.</p>
        </div>
      </div>
    </div><br>
    <div class="container opinion">
      <h2 class="font-weight-bold">Opinions</h2>
      <div class="row mt-4">
        <div class="col-3 text-center">
          <img id="client" class=" foto rounded-circle" src="../assets/dude.jpg" alt="cliente contento">
        </div>
        <div class="col-3">
          <p class="font-italic">" I would recommend it to everybody! It´s nice, fast and efficient"</p>
        </div>
        <div class="col-3 text-center">
         <img id="client" class="foto rounded-circle" src="../assets/enri.jpg" alt="cliente contento">
        </div>
        <div class="col-3">
          <p class="font-italic">"Two months ago I was so confused when I wanted to buy my first bike and Buybike helped me to take the best decision "</p>
        </div>
      </div>
    </div>

    <section class="container company mt-4">
      <div class="row">
        <div class="col-6">
          <h2 class="font-weight-bold">Who we are</h2>
          <p>Buybike appears as a final project of a web developer course taught in Málaga by the EOI, we are a young company in growth and our goal is to help the society to find the bike of his dream on an easy way. We love riders! we love bikes!</p>
        </div>
        <div class="col-6 mt-2">
          <img class="foto" src="../assets/company.jpg" alt="quienes somos">
        </div>
      </div>
    </section>
</div>
	 
</template>

<script>

  import { dbUsersRef } from '../firebase'
  import { dbFilterOneRef } from '../firebase';
	import { dbFilterTwoRef } from '../firebase';
	import { dbFilterThreeRef } from '../firebase';	
	import { dbFinalRef } from '../firebase'
	import { dbBrandRef } from '../firebase'
	import { dbSortedByPrice } from '../firebase'
	import { dbSortedByPower } from '../firebase'
  
  export default {
    data () {
      return {
        
      }
    },
    methods: {
      
    },
    created() {
      dbUsersRef.remove();
      dbFilterOneRef.remove();
      dbFilterTwoRef.remove();
      dbFilterThreeRef.remove();
      dbFinalRef.remove();
      dbSortedByPrice.remove();
      dbSortedByPower.remove();
    },
    firebase: {
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
  
  .card-img-top {
    height: 250px;

  }
  .foto {
    height: 150px;
    margin-bottom: 20px;
  }
  
  h1, h2, h5{
    font-family: 'Raleway', sans-serif;
  }
  .opinion {
    background-color:#F7F8FD;
    margin-bottom: 20px;
  }
  .company {
    margin-bottom: 5px;
  }
  
</style>
