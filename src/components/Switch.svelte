<script lang="ts">
    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    function change() {
        dispatch('change', {switchValue: switchValue});
    }

    let switchValue = true;
</script>

<label>
    <input type=checkbox bind:checked={switchValue} on:change={change}>
    <slot></slot>
</label>
