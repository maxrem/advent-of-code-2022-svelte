<script lang="ts">
    import TestSwitch from "../../components/TestSwitch.svelte";
    import BackToHome from "../../components/BackToHome.svelte";

    function testSwitchChanged(event?: { detail: { test: boolean } }) {
        let test = true;
        if (event !== undefined) {
            test = event.detail.test;
        }

        calculate(test);
    }

    function calculate(test: boolean) {

    }

    calculate(true);

</script>

<h1>Day 2: Calorie Counting</h1>

<TestSwitch on:change={testSwitchChanged}/>

<p>Test answer is: ?</p>

<BackToHome/>
