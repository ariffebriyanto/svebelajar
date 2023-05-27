<script>
    import { onMount } from "svelte";
//display data from api
    let posts = [];

    onMount(() => {
        fetch("https://jsonplaceholder.typicode.com/posts")
            .then((response) => response.json())
            .then((result) => (posts = result));
    });

    const postData = {
        userId: "",
        title: "",
        body: "",
    };
    //post
    function formHandler(event) {
        event.preventDefault();
        //console.log(postData);
        fetch("https://jsonplaceholder.typicode.com/posts/", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({
                postData,
            }),
        })
            .then((response) => response.json())
            .then((data) => {
                console.log(data);
                data.postData.id = data.id;
                posts = [data.postData, ...posts];
            })
            .catch((err) => {
                console.log(err.message);
            });
    }

    //delete
    function formHandlerdelete(id) {
        fetch("https://jsonplaceholder.typicode.com/posts/" + id, {
            method: "DELETE",
        })
            .then((response) => {
                if (response.status === 200) {
                    posts = posts.filter((post) => {
                        return post.id !== id;
                    });
                } else {
                    return;
                }
            })
            .then((result) => console.log(result));
    }
</script>

<section>
    <form>
        <div>
            <label for="userId">UserID:</label>
            <input type="text" id="userId" bind:value={postData.userId} />
        </div>
        <div>
            <label for="title">Title: </label>
            <input type="text" id="title" bind:value={postData.title} />
        </div>
        <div>
            <label for="body">Body: </label>
            <textarea id="body" rows="6" cols="22" bind:value={postData.body} />
        </div>
        <button on:click={formHandler}>Create Post</button>
    </form>
</section>

{#each posts as post (post.id)}
    <h2>({post.id}) {post.title}</h2>
    <p>{post.body}</p>
    <button on:click={formHandlerdelete(post.id)}>Delete Post</button>
    <hr />
{:else}
    <h2>Loading...</h2>
{/each}

<style>
    section {
        height: 100vh;
        display: grid;
        justify-items: center;
        padding-top: 40px;
    }
    div {
        margin: 24px auto;
    }
    label {
        font-weight: bolder;
        display: block;
        margin-bottom: 4px;
    }
</style>
