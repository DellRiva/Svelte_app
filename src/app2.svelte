<script>
    let stringToRender = "";
    let displayInfoMessage = false;
    import {slide, fade} from "svelte/transition";

    let count = 0;

    import {tweened} from 'svelte/motion';
    import {backInOut} from 'svelte/easing';

    function handleClick(){
        count += 1;
    }
    $: square = count ** 2;
    $: squareMinus = square -1;

    let cities = [
        {
            id:"321",
            name:"london"
        }
    ]

    import {writable} from 'svelte/store';

    const proges = tweened(0, {
        duration: 2000,
        easing: backInOut
    });
</script>

<style>
    textarea {
        width: 100%;
        height: 12rem;
    }

    progress{
        display: block;
        width: 100%;
    }

</style>

<textarea bind:value={stringToRender} />

<div>{@html stringToRender}</div>

<form action="">
    <div class="name-field">
        <label for="name">Name </label>
        <input type="text" name="name">
    </div>
    <div class="surname-field">
        <label for="surname">surname</label>
        <input type="text" name="name">
    </div>
    <div>
        <label for="">    
        <input type="checkbox" bind:checked={displayInfoMessage} />
            do you want to give me a milion dollars ?
        </label>
    </div>
</form>

{#if displayInfoMessage}
    <h1 transition:fade>Thank Bro </h1>
    {/if}

<button on:click={handleClick}>Counter : {count}</button>
<h1>Square of the counter is {square}</h1>
<h1>Square minus of the counter is {squareMinus}</h1>

<h1>European cities</h1>
<ul>
    {#each cities as city}
    <li>{city.name}</li>
    {/each}
</ul>

<h1>Installing windows 95..</h1>
<progress value={$proges} />
<sub>2 weeks remaining </sub>

<button on:click={()=> proges.set(0)}>0%</button>
<button on:click={()=> proges.set(0.75)}>75%</button>
<button on:click={()=> proges.set(1)}>100%</button>

{#if $proges === 1.0}
<h1>Windows installed , Horay </h1>
{/if}