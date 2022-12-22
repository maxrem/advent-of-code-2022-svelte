<script lang="ts">
    import Switch from "../../components/Switch.svelte";
    import BackToHome from "../../components/BackToHome.svelte";

    import testData from "../../data/02-rock-paper-scissors/test.txt?raw";
    import realData from "../../data/02-rock-paper-scissors/real.txt?raw";

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

    let points = 0;
    function calculateProblem1(isTest: boolean) {

        /*
          A = rock
          B = paper
          C = scissors

          X = rock
          Y = paper
          Z = scissors

          Rock defeats Scissors, Scissors defeats Paper, and Paper defeats Rock

          The score for a single round is the score for the shape you selected (1 for Rock, 2 for Paper, and 3 for
          Scissors) plus the score for the outcome of the round (0 if you lost, 3 if the round was a draw, and 6 if you
          won).
         */

        let rows;
        if (isTest) {
            rows = testRows;
        } else {
            rows = realRows;
        }

        points = 0;
        const matchPoints = new Map();
        matchPoints.set('X', 1);
        matchPoints.set('Y', 2);
        matchPoints.set('Z', 3);

        for (let i = 0; i < rows.length; i++) {
            if (rows[i].length <= 0) {
                continue;
            }

            const match = rows[i].split(" ");

            points += matchPoints.get(match[1]);

            if (
                match[0] == 'A' && match[1] == 'Z' ||
                match[0] == 'C' && match[1] == 'Y' ||
                match[0] == 'B' && match[1] == 'X'
            ) {
                continue;
            }

            if (
                match[0] == 'C' && match[1] == 'X' ||
                match[0] == 'B' && match[1] == 'Z' ||
                match[0] == 'A' && match[1] == 'Y'
            ) {
                points += 6;
                continue;
            }

            points += 3;
        }
    }

    function calculateProblem2(isTest: boolean) {
        // TODO implement
        points = -1;
    }

    calculate();

</script>

<h1>Day 2: Rock Paper Scissors</h1>

<Switch on:change={testSwitchChanged}>Test</Switch>
<Switch on:change={problemSwitchChanged}>Problem 1</Switch>

<p>Answer is: {points}</p>

<BackToHome/>
