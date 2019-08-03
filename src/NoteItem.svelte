<script>
    import marked from 'marked'

    export let text;
    export let dateTime;
</script>

<style>
    li {
        list-style: none;
        padding: 10px;
        border: 1px solid #ddd;
        margin: 10px;
        max-width: 300px;
        border-radius: 4px;
    }
</style>

<li>
    <p>{@html marked(text)}</p>
    <pre>{dateTime}</pre>
</li>
