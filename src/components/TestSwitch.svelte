<script lang="ts">
    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    function change() {
        dispatch('change', {isTest: isTest});
    }

    let isTest = true;
</script>

<label>
    <input type=checkbox bind:checked={isTest} on:change={change}>
    Test
</label>
