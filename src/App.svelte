<script>
	export let name;
    import NoteItem from './NoteItem.svelte';
    import Footer from './Footer.svelte';   

    let text = '';
    let notes = [];
    
    let localNotes = localStorage.getItem('notes');
    if(localNotes) { notes = [...JSON.parse(localNotes)]; }

    function saveNote() {
        notes = [...notes, {
            text,
            dateTime: new Date().toUTCString()
        }];
        localStorage.setItem('notes', JSON.stringify(notes))
        text = '';
    }

    function deleteNote(e) {
        let i = e.detail.i
        alert(`event triggered for index: ${i}`)
        notes = [...notes.slice(0, i), ...notes.slice(i+1)]
    }

    function clearNotes() {
        notes = [];
        localStorage.setItem('notes', '');
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
{#each notes as note, i}
<NoteItem {...note} i={i} on:deletenote={deleteNote}/>
{/each}
</ul>
<form class="container">
<textarea placeholder="Take a note..." bind:value={text}/>
<button type="submit" on:click|preventDefault={saveNote}>Save</button>
</form>
<button on:click={clearNotes}>Clear Notes</button>
<Footer />
