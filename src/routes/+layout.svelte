<script>
 //enable global style over the whole sveltekit app.
	import '../app.css'
 	import Header from '../components/Header.svelte'
 	import Footer from '../components/Footer.svelte'
</script>


<div class="container mx-auto px-40 py-10">
	<Header/>
	<slot/>
	<Footer/>
</div>