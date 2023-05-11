
<script lang="ts">
	let name: string = 'world';
    let angka1: int=1;
    let angka2: int=2;
    import { Link } from 'svelte-routing'
 
</script>


<main>
    
	<h1>Hello {name}!</h1>
	<p>Hasil {angka1 + angka2}
        <nav>
            <Link to="/">Home</Link>
            <Link to="/Details/">Detail</Link>
            <Link to="/product/1">Recommended Product</Link>
        </nav>
    
</main>

<style lang="scss">
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;

		h1 {
			color: blue;
			text-transform: uppercase;
			font-size: 4em;
			font-weight: 100;
		}

		@media (min-width: 640px) {
			max-width: none;
		}
	}
</style>
