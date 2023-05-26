<script>
    import { Router, Route } from 'svelte-routing'
    import Home from './pages/Home.svelte'
    import Details from './pages/Details.svelte'
	import Products from './pages/Products.svelte'
	import Api from './pages/api.svelte'
</script>

<Router>
    <Route component={Home} />
    <Route path="/Details" component={Details} />
	<Route path="/Api" component={Api} />
    <Route path="/product/:id" let:params>
        <Products id={params.id} />
    </Route>
</Router>


<!-- <script lang="ts">
	let name: string = 'world';
</script>

<main>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>

<style lang="scss">
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;

		h1 {
			color: #ff3e00;
			text-transform: uppercase;
			font-size: 4em;
			font-weight: 100;
		}

		@media (min-width: 640px) {
			max-width: none;
		}
	}
</style> -->
