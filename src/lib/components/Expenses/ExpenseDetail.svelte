<script>
    import { createEventDispatcher } from "svelte";
    import {blur, scale, fade, fly, slide} from "svelte/transition";
    /// props
    export let id;
    export let name = "";
    export let amount = 0;
    //// variables
    const dispatch = createEventDispatcher();
    let displayAmount = false;

    const toggleAmount = () => {
        displayAmount = !displayAmount;
    };
    const dispatchDelete = (e) => {
        dispatch("onDelete", { id });
    };
    const dispatchEdit = (e) => {
        dispatch("onEdit", { id });
    };
</script>

<article class="single-expense">
    <div class="expense-info">
        <h2>
            {name}
            <button class="amount-btn" on:click={toggleAmount}>
                <i class="fas fa-caret-down" />
            </button>
        </h2>
        {#if displayAmount}
        <!-- <h4 transition:blur>amount: ${amount}</h4> -->
            <!-- <h4 transition:scale>amount: ${amount}</h4> -->
            <!-- <h4 transition:slide>amount: ${amount}</h4> -->
            <!-- <h4 transition:fade>amount: ${amount}</h4> -->
            <h4 transition:fly={{x: 300, y: 0, duration: 500, delay: 150}}>amount: ${amount}</h4>
        {/if}
    </div>
    <div class="expense-buttons">
        <button class="expense-btn edit-btn" on:click={dispatchEdit}>
            <i class="fas fa-pen" />
        </button>
        <button class="expense-btn delete-btn" on:click={dispatchDelete}>
            <i class="fas fa-trash" />
        </button>
    </div>
</article>
