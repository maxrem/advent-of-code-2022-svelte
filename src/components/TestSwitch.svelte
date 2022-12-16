<script lang="ts">
    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    function change() {
        dispatch('change', {test: test});
    }

    let test = true;
</script>

<label>
    <input type=checkbox bind:checked={test} on:change={change}>
    Test
</label>
