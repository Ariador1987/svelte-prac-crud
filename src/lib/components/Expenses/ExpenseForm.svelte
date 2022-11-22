<script>
    import Title from "../Title.svelte";
    import { createEventDispatcher } from "svelte";

    //// variables
    const dispatch = createEventDispatcher();
    export let name = "";
    export let amount = null;
    export let id = null;

    export let isEditing = false;

    //// reactives
    $: isEmpty = !name || !amount;

    //// functions
    const handleSubmit = (e) => {
        // dispatch("createExpense", { name, amount });
        if (isEditing) {
            dispatch("editItem", { name, id, amount });
            clearFields();
            return;
        }
        console.log("not editing");
    };
    const clearFields = () => {
        name = "";
        amount = null;
        id = null;
    };
</script>

<section class="form">
    <Title title="Add expense" />
    <form class="expense-form" on:submit|preventDefault={handleSubmit}>
        <div class="form-control">
            <label for="name">name</label>
            <input bind:value={name} type="text" id="name" />
        </div>
        <div class="form-control">
            <label for="amount">amount</label>
            <input bind:value={amount} type="number" id="amount" />
        </div>
        {#if isEmpty}
            <p class="form-empty">Please fill out all form fields</p>
        {/if}
        <button type="submit" class="btn btn-block">Add expense</button>
        <button
            disabled={isEmpty}
            type="button"
            class="close-btn"
            class:disabled={isEmpty}
        >
            <i class="fas fa-times" />
            Close
        </button>
    </form>
</section>
