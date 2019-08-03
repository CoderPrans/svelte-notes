<script>
	export let name;
    import NoteItem from './NoteItem.svelte';
    import Footer from './Footer.svelte';   

    let text = '';
    let notes = [];

    function saveNote() {
        notes = [...notes, {
            text,
            dateTime: new Date().toUTCString()
        }];
        text = '';
    }
</script>

<style>
	h1 {
		color: purple;
        text-align: center;
	}
    button {
        cursor: pointer;
        margin: 0 25px;
    }
    .container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    textarea {
        width: 300px;
        height: 200px;
        resize: none;
        padding: 0.5em;
        transition: all 0.5s ease;
        margin: 25px;
    }
    ul {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        padding: 0;
    }
    /*textarea:focus {
        height: 8em;
    }*/
</style>

<h1>{name}!</h1>
<ul class="preview">
{#each notes as note}
<NoteItem {...note}/>
{/each}
</ul>
<form class="container">
<textarea placeholder="Take a note..." bind:value={text}/>
<button type="submit" on:click|preventDefault={saveNote}>Save</button>
</form>
<Footer />
