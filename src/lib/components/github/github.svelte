<script>
    import { onMount } from "svelte";
    const apiUrl = "https://api.github.com/users";
    let users = [];
    let isLoading = true;

    onMount(async () => {
        let response = await fetch(apiUrl);
        let data = await response.json();
        users = data;
        isLoading = false;
    })
</script>

<div>
    {#if isLoading}
       <h2>Loading...</h2>
    {:else}
        <section>
            {#each users as user (user.id)}
            <article>
                <img src={user.avatar_url} alt={user.login} />
                <div class="user-info">
                    <h3>User: {user.login}</h3>
                    <a href={user.html_url} class="btn-primary" target="_blank" rel="noreferrer">
                        github url
                    </a>
                </div>
            </article>
            {/each}
        </section>
    {/if}
    
</div>

<style>
    article {
        margin-bottom: 1.5rem;
    }
    h2 {
        text-align: center;
    }
    img {
        height: 200px;
        width: 200px;
        border-radius: 50%;
    }
    btn {
        cursor: pointer;
    }
</style>