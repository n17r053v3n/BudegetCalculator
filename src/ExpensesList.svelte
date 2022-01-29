<script>
    import Title from "./Title.svelte";
    import Expense from "./Expense.svelte";
    export let expenses = [];
    
</script>

<section>
    <Title title="Expense list"></Title>
    <ul>
        {#each expenses as expense, index}
            <Expense {...expense} />
            {:else}
            <h2>Currently you have no expenses</h2>
        {/each}
    </ul>
</section>