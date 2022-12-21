<script lang="ts">
    import BackToHome from "../../components/BackToHome.svelte";
    import Switch from "../../components/Switch.svelte";

    import testData from "../../data/01-calorie-counting/test.txt?raw";
    import realData from "../../data/01-calorie-counting/real.txt?raw";

    let highestSum = 0;

    const testRows = testData.split("\n");
    const realRows = realData.split("\n");

    let isTest = true;
    let problemFirst = true;

    function testSwitchChanged(event?: { detail: { switchValue: boolean } }) {
        if (event !== undefined) {
            isTest = event.detail.switchValue;
        }

        calculate();
    }

    function problemSwitchChanged(event?: { detail: { switchValue: boolean } }) {
        if (event !== undefined) {
            problemFirst = event.detail.switchValue;
        }

        calculate();
    }

    function calculate() {
        if (problemFirst) {
            calculateProblem1(isTest);
            return;
        }

        calculateProblem2(isTest);
    }

    function calculateProblem1(isTest: boolean) {
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

    const numericFunction = (x, y) => x - y;

    function calculateProblem2(isTest: boolean) {
        let rows;
        if (isTest) {
            rows = testRows;
        } else {
            rows = realRows;
        }

        let sumList = [-1, -1, -1];
        let sum = 0;
        for (let i = 0; i < rows.length; i++) {
            if (i > 0 && rows[i] === "") {
                if (sum > sumList[0]) {
                    sumList[0] = sum;
                    sumList.sort(numericFunction);
                }
                sum = 0;
                continue;
            }

            sum += parseInt(rows[i]);
        }

        if (sum > sumList[0]) {
            sumList[0] = sum;
            sumList.sort(numericFunction);
        }

        highestSum = sumList.reduce((x, y) => x + y, 0);
    }

    calculate();
</script>

<h1>Day 1: Calorie Counting</h1>

<Switch on:change={testSwitchChanged}>Test</Switch>
<Switch on:change={problemSwitchChanged}>Problem 1</Switch>

<p>Test answer is: {highestSum}</p>

<BackToHome/>
