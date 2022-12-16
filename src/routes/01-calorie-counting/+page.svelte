<script lang="ts">
    import BackToHome from "../../components/BackToHome.svelte";
    import testData from "../../data/01-calorie-counting/test.txt?raw";
    import realData from "../../data/01-calorie-counting/real.txt?raw";
    import TestSwitch from "../../components/TestSwitch.svelte";

    let highestSum = 0;

    const testRows = testData.split("\n");
    const realRows = realData.split("\n");

    function testSwitchChanged(event?: { detail: { test: boolean } }) {
        let test = true;
        if (event !== undefined) {
            test = event.detail.test;
        }

        calculate(test);
    }

    function calculate(test: boolean) {
        let rows;
        if (test) {
            rows = testRows;
        } else {
            rows = realRows;
        }
        let sum = 0;
        highestSum = 0;
        for (let i = 0; i < rows.length; i++) {
            if (i > 0 && rows[i] === "") {
                highestSum = Math.max(sum, highestSum);
                sum = 0;
                continue;
            }

            const row: number = parseInt(rows[i]);
            sum += row;
        }

        highestSum = Math.max(sum, highestSum);
    }

    calculate(true);
</script>

<h1>Day 1: Calorie Counting</h1>

<TestSwitch on:change={testSwitchChanged}/>

<p>Test answer is: {highestSum}</p>

<BackToHome/>
