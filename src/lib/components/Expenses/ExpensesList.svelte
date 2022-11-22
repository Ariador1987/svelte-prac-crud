<script>
    import App from "../../../App.svelte";
    import SectionTitle from "../Title.svelte";
    import ExpenseDetail from "./ExpenseDetail.svelte";

    export let expenses = [];
</script>

<section>
    <SectionTitle title="expense list" />
    <ul>
        {#each expenses as expense, index (expense.id)}
            <ExpenseDetail {...expense} on:onDelete on:onEdit />
        {:else}
            <h2>No expenses added to the list</h2>
        {/each}
    </ul>
</section>
