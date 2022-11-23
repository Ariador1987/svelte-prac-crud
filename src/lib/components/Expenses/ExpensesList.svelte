<script>
    import App from "../../../App.svelte";
    import { fly } from "svelte/transition";
    import { flip } from "svelte/types/runtime/animate";
    import "./types/runtime/animate";
    import SectionTitle from "../Title.svelte";
    import ExpenseDetail from "./ExpenseDetail.svelte";

    export let expenses = [];
</script>

<section>
    <SectionTitle title="expense list" />
    <ul>
        {#each expenses as expense, index (expense.id)}
            <div in:fly={{x: 200, delay: (index + 1) * 700}} out:fly animate:flip>
                <ExpenseDetail {...expense} on:onDelete on:onEdit />
            </div>
        {:else}
            <h2>No expenses added to the list</h2>
        {/each}
    </ul>
</section>
