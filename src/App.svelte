<script>
	import { setContext } from "svelte";
	// components
	import Navbar from "./Navbar.svelte";
	import ExpensesList from "./ExpensesList.svelte";
	import Expense from "./Expense.svelte";
	import Totals from "./Totals.svelte"
	import ExpenseForm from "./ExpenseForm.svelte"
	//	data
	import expendesData from "./expenses";
	// variables
	let expenses = [...expendesData];
	//reactive
	$: total = expenses.reduce((acc,curr)=>{/*console.log({acc, amount:curr.amount});*/ return (acc += curr.amount)},0)
	// functions
	function removeExpense(id){
		expenses = expenses.filter(item => item.id !== id);
	}
	function clearExpenses(){
		expenses = [];
	}
	// context
	setContext('remove', removeExpense)
</script>

<Navbar />
<main class="content">
	<ExpenseForm/>
	<Totals title="total expenses" {total}/>
	<ExpensesList {expenses}  />
	<button type button class="btn btn-primary btn-block" on:click={clearExpenses}>
		clear expenses
	</button>
</main>