<script lang="js">
    import { onMount, afterUpdate } from "svelte";
    //// components
    import Navbar from "./lib/components/Navbar.svelte";
    import Title from "./lib/components/Title.svelte";
    import Totals from "./lib/components/Totals.svelte";
    import ExpensesList from "./lib/components/Expenses/ExpensesList.svelte";
    import ExpenseForm from "./lib/components/Expenses/ExpenseForm.svelte";
    import Modal from "./lib/components/Modal.svelte";
    //// data
    // import expensesData from "./lib/data/data";
    // local copy of the data
    let expenses = [];
    //// variables
    $: total = calculateTotals(expenses);
    // editing variables
    let setName = "";
    let setAmount = null;
    let setId = null;

    // možemo ovo napravit reaktivnom vrijednošću i postavit je na setId
    // ako je setId null, onda je isEditing automatski false i netrebamo propdrillat ga
    $: isEditing = false;
    let isShown = false;

    //// functions
    const calculateTotals = (expensesArr) => {
        if (!expensesArr || expensesArr.length === 0) {
            return 0;
        }
        return expensesArr.reduce(
            (cache, currVal) => (cache += currVal.amount),
            0
        );
    };
    const handleDelete = (e) => {
        const { id } = e.detail;
        expenses = expenses.filter((x) => x.id !== id);
    };
    const handleEdit = (e) => {
        // Loads it into UI and notifies form we're editing
        const { id } = e.detail;
        const itemToModify = expenses.find((item) => item.id === id);
        setAmount = itemToModify.amount;
        setId = itemToModify.id;
        setName = itemToModify.name;
        isEditing = true;
        displayForm();        
    };
    const clearExpenses = () => {
        expenses = [];

    };
    const addExpense = (e) => {
        const { name, amount } = e.detail;
        expenses = [{ id: Math.random(), name, amount }, ...expenses];
    };
    const editExpense = (e) => {
        const { id, name, amount } = e.detail;
        expenses = expenses.map((item) => {
            if (item.id === id) {
                return { ...item, id, name, amount };
            }
            return item;
        });
    };
    const setDefaultState = () => {
        isEditing = false;
        setName = "";
        setAmount = null;
        setId = null;
    };
    const displayForm = () => {
        isShown = true;
    }
    const hideForm = () => {
        isShown = false;
    }

    // local storage
    const setLocalStorage = () => {
        localStorage.setItem("expenses" , JSON.stringify(expenses));
    }

    onMount(() => {
        let expensesfromLS;
        if (localStorage.getItem("expenses")) {
            expensesfromLS = JSON.parse(localStorage.getItem("expenses"))
        } else {
            expensesfromLS = [];
        }
        expenses = expensesfromLS;
    })
    afterUpdate(() => {
        console.log("after update")
        setLocalStorage();
    })
</script>

<Navbar {displayForm}/>
<main class="content">
    {#if isShown}
        <Modal>
            <ExpenseForm
                {hideForm}
                on:createExpense={addExpense}
                on:editItem={editExpense}
                {isEditing}
                name={setName}
                id={setId}
                amount={setAmount}
            />
        </Modal>
    {/if}
    <Totals title="total expenses" {total} />
    <ExpensesList
        {expenses}
        on:onDelete={handleDelete}
        on:onEdit={handleEdit}
    />
    <button
        type="button"
        class="btn btn-primary btn-block"
        on:click={clearExpenses}>Clear Expenses</button
    >
</main>