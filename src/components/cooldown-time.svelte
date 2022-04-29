<script lang="ts">
    export let minutes;
    export let seconds;

    function pad(n) {
        return n < 10 ? `0${n}` : n;
    }
</script>

<div>
    {minutes}m{pad(seconds)}s
</div>
