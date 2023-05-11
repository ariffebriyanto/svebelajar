<script>
    import { navigate } from 'svelte-routing'

    export let id

    // const product = product.find(product => product.id)
console.log(id)
    if (!id) {
         navigate('/')
     }
</script>
<p>
products view for: {id}
</p>