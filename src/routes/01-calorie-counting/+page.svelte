<script lang="ts">
    import BackToHome from "../../components/BackToHome.svelte";
    import TestSwitch from "../../components/TestSwitch.svelte";

    import testData from "../../data/01-calorie-counting/test.txt?raw";
    import realData from "../../data/01-calorie-counting/real.txt?raw";

    let highestSum = 0;

    const testRows = testData.split("\n");
    const realRows = realData.split("\n");

    // TODO 2nd assignment

    function testSwitchChanged(event?: { detail: { isTest: boolean } }) {
        let isTest = true;
        if (event !== undefined) {
            isTest = event.detail.isTest;
        }

        calculate(isTest);
    }

    function calculate(isTest: boolean) {
        let rows;
        if (isTest) {
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
