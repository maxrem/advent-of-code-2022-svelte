<script lang="ts">
    import TestSwitch from "../../components/TestSwitch.svelte";
    import BackToHome from "../../components/BackToHome.svelte";

    import testData from "../../data/02-rock-paper-scissors/test.txt?raw";
    import realData from "../../data/02-rock-paper-scissors/real.txt?raw";

    const testRows = testData.split("\n");
    const realRows = realData.split("\n");

    function testSwitchChanged(event?: { detail: { isTest: boolean } }) {
        let isTest = true;
        if (event !== undefined) {
            isTest = event.detail.isTest;
        }

        calculate(isTest);
    }

    let points = 0;
    function calculate(isTest: boolean) {
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
            console.log('new round');
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

    calculate(true);

</script>

<h1>Day 2: Rock Paper Scissors</h1>

<TestSwitch on:change={testSwitchChanged}/>

<p>Test answer is: {points}</p>

<BackToHome/>
