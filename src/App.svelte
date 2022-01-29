<script>
	import { setContext } from "svelte";
	// components
	import Navbar from "./Navbar.svelte";
	import ExpensesList from "./ExpensesList.svelte";
	import Expense from "./Expense.svelte";

	//	data
	import expendesData from "./expenses";
	// variables
	let expenses = [...expendesData];
	// functions
	function removeExpense(id){
		expenses = expenses.filter(item => item.id !== id);
	}
	// context
	setContext('remove', removeExpense)
</script>

<Navbar />
<main class="content">
	<ExpensesList {expenses}  />
</main>