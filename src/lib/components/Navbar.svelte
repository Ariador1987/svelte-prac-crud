<script>
    export let displayForm = () => {};
</script>

<nav class="nav">
    <div class="nav-center">
        <h1 class="nav-title">Budget calculator</h1>
        <button type="button" class="nav-btn" on:click="{displayForm}">
            <i class="far fa-plus-square" />
            Add Item
        </button>
    </div>
</nav>
