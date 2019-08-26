<script>
    import marked from 'marked'
    import { createEventDispatcher } from 'svelte'

    let dispatch = createEventDispatcher();

    function delEvent(i) {
        dispatch("deletenote", { i })
    } 

    export let text;
    export let dateTime;
    export let i;
</script>

<style>
    li {
        list-style: none;
        padding: 0 20px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        border: 1px solid #ddd;
        margin: 0 10px;
        max-width: 300px;
        border-radius: 4px;
    }
    .delete-icon {
        font-size: 20px;
        cursor: pointer;
        margin: 0;
    }
    .note-info {
        display: flex; 
        justify-content: space-between; 
        align-items: center;
        width: 100%;
    }
</style>

<li>
    <p>{@html marked(text)}</p>
    <div class="note-info">
    <pre>{dateTime}</pre>
    <p class="delete-icon" on:click={() => delEvent(i)}>🗑️</p>
    </div>
</li>
