<script>
    import Title from "../Title.svelte";
    import { createEventDispatcher } from "svelte";

    //// variables
    const dispatch = createEventDispatcher();
    export let name = "";
    export let amount = null;
    export let id = null;
    export let setDefaultState = () => {};

    export let isEditing = false;
    export let showForm = false;

    //// reactives
    $: isEmpty = !name || !amount;

    //// functions
    const handleSubmit = (e) => {
        if (isEmpty) return;
        if (isEditing) {
            dispatch("editItem", { name, id, amount });
        } else {
            dispatch("createExpense", { name, amount });
        }
        // handles reset for this component
        clearFields();
        // handles reset for app component in case 
        setDefaultState();
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
        <button type="submit" class="btn btn-block">{isEditing ? "Edit" : "Add"} expense</button>
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
