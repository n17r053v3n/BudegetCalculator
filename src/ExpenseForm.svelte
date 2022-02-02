<script>
    // import { onMount, onDestroy, beforeUpdate, afterUpdate } from "svelte";
    // onMount(() => {
    //     console.log("form has mounted");
    // });
    // onDestroy(() => {
    //     console.log("form has destroyed");
    // });
    // beforeUpdate(() => {
    //     console.count("before update");
    // });
    // afterUpdate(() => {
    //     console.count("after update");
    // });
    import Title from "./Title.svelte";
    export let name = "";
    export let amount = null;
    export let addExpese;
    export let isEditing;
    export let editExpense;
    export let closeForm;
    //$: console.log({name, amount})
    $: isEmty = !name || !amount;
    function handleSubmit() {
        if (isEditing) {
            editExpense({ name, amount });
        } else {
            addExpese({ name, amount });
        }
        name = "";
        amount = null;
        closeForm();
    }
</script>

<section class="form">
    <Title title="add expense" />
    <form class="expense-form" on:submit|preventDefault={handleSubmit}>
        <div class="form-control">
            <label for="name">name</label>
            <input type="text" id="name" bind:value={name}/>
        </div>
        <div class="form-control">
            <label for="amount">amount</label>
            <input type="number" id="amount" bind:value={amount} />
        </div>
        {#if isEmty}
            <p class="form-empty">please fill out our form fields</p>
        {/if}
        <button
            type="submit"
            class="btn btn-block"
            class:disabled={isEmty}
            disabled={isEmty}
        >
            {#if !isEditing}
                add expense
            {:else}
                edit expense
            {/if}
        </button>
        <button type="button" class="close-btn" on:click={closeForm}>
            <i class="fas fa-times" /> close
        </button>
    </form>
</section>
