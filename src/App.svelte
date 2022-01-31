<script>
	import { setContext } from "svelte";
	// components
	import Navbar from "./Navbar.svelte";
	import ExpensesList from "./ExpensesList.svelte";
	import Expense from "./Expense.svelte";
	import Totals from "./Totals.svelte";
	import ExpenseForm from "./ExpenseForm.svelte";
	//	data
	import expendesData from "./expenses";
	// variables
	let expenses = [...expendesData];
	// set values
	let setName = "";
	let setAmount = null;
	let setId = null;
	// 	toggle form vars
	let isFormOpen = false;
	//reactive
	$: isEditing = setId ? true : false;
	$: total = expenses.reduce((acc, curr) => {
		/*console.log({acc, amount:curr.amount});*/ return (acc += curr.amount);
	}, 0);
	// functions
	function removeExpense(id) {
		expenses = expenses.filter((item) => item.id !== id);
	}
	function clearExpenses() {
		expenses = [];
	}
	function addExpese({ name, amount }) {
		let expense = { id: Math.random() * Date.now(), name, amount };
		expenses = [expense, ...expenses];
	}
	function setModifiedExpense(id) {
		let expense = expenses.find((item) => item.id === id);
		setId = expense.id;
		setName = expense.name;
		setAmount = expense.amount;
		openForm();
	}
	function editExpense({ name, amount }) {
		expenses = expenses.map((item) => {
			return item.id === setId ? { ...item, name, amount } : { ...item };
		});
		setId = null;
		setName = "";
		setAmount = null;
	}
	function openForm() {
		isFormOpen = true;
		console.log(isFormOpen);
	}
	function closeForm() {
		isFormOpen = false;
		setName = "";
		setAmount = null;
		setId = null;
	}
	// context
	setContext("remove", removeExpense);
	setContext("modify", setModifiedExpense);
</script>

<Navbar {openForm}/>
<main class="content">
	{#if isFormOpen}
		<ExpenseForm
			{addExpese}
			name={setName}
			amount={setAmount}
			{isEditing}
			{editExpense}
			{closeForm}
		/>
	{/if}
	<Totals title="total expenses" {total} />
	<ExpensesList {expenses} />
	<button
		type
		button
		class="btn btn-primary btn-block"
		on:click={clearExpenses}
	>
		clear expenses
	</button>
</main>
