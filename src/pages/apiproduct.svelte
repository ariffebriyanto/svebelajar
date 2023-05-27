<script>
    import { onMount } from "svelte";

    let posts = [];

    onMount(() => {
        fetch("https://dummyjson.com/products")
            .then((response) => response.json())
            .then((result) => (posts = result.products));
    });
    let postdata1=[];
    const postData = {
       title:"",
           
    };
    function formHandler(event) {
        event.preventDefault();
        //console.log(postData);

        fetch("https://dummyjson.com/products/add", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify({
               title: postData.title,
                /* other product data */
            }),
        })
            .then((response) => response.json())
            .then((data) => {
                console.log(data);

                
                posts = [data, ...posts];
                
            })
            .catch((err) => {
                console.log(err.message);
            });
    }
</script>

<section>
    <form>
        <div>
            <label for="title">Title: </label>
            <input type="text" id="title" bind:value={postData.title} />
        </div>

        <button on:click={formHandler}>Create Post</button>
    </form>
</section>
{#each posts as post}
    <h2>({post.title})</h2>

    <hr />
{:else}
    <h2>Loading...</h2>
{/each}
