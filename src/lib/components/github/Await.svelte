<script>
    const apiUrl = "https://api.github.com/users";

    const getUsers = async () => {
        let response = await fetch(apiUrl);
        let users = await response.json();
        return users;
    }
</script>

<section>
    {#await getUsers()}
        <h1>Loading...</h1>
    {:then users}
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
        {:catch error} 
        <p>Something went wrong {error.message}</p>
    {/await}
</section>