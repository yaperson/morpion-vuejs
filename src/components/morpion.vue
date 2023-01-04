<script>
export default {
    data() {
        return {
            players: {
                player1: {
                    id: 1,
                    name: "player1",
                    score: 0,
                    isPlay: true,
                    cases: [],
                },
                player2: {
                    id: 1,
                    name: "player2",
                    score: 0,
                    isPlay: true,
                    cases: [],
                },
            },
            party: {
                state: true,
            },
        };
    },

    methods: {
        // set players scores and party state for start or restart party
        initGame() {
            window.location.reload();
        },

        newParty() {
            this.party.state = true;
        },

        // Action when user play
        changeValue(event) {
            let targetId = event.currentTarget.id;
            let row = event.currentTarget.parentNode;
            let player1 = this.players.player1;
            let player2 = this.players.player2;

            if (this.party.state === true) {
                if (player1.isPlay == true) {
                    if (!row.querySelector("#" + targetId).innerText) {
                        row.querySelector("#" + targetId).innerText = "X";
                        player1.cases.push({ case: targetId, row: row.id });
                        this.changePlayer();
                        this.checkScore(player1);
                    }
                } else {
                    if (!row.querySelector("#" + targetId).innerText) {
                        row.querySelector("#" + targetId).innerText = "O";
                        player2.cases.push({ case: targetId, row: row.id });
                        this.changePlayer();
                        this.checkScore(player2);
                    }
                }
            }
        },

        // Change player statut (isPlay?)
        changePlayer() {
            if (this.players.player1.isPlay == true) {
                this.players.player1.isPlay = false;
                this.players.player2.isPlay = true;
            } else {
                this.players.player1.isPlay = true;
                this.players.player2.isPlay = false;
            }
        },

        // Check score of last player
        checkScore(player) {
            let angleTG = 0;
            let midleT = 0;
            let angleTD = 0;

            let midleG = 0;
            let midleC = 0;
            let midleD = 0;

            let angleBG = 0;
            let midleB = 0;
            let angleBD = 0;

            for (let elem in player.cases) {
                let playerCases = player.cases[elem];

                if (playerCases.case == "case1" && playerCases.row == "row1") angleTG++;
                if (playerCases.case == "case2" && playerCases.row == "row1") midleT++;
                if (playerCases.case == "case3" && playerCases.row == "row1") angleTD++;
                if (playerCases.case == "case1" && playerCases.row == "row2") midleG++;
                if (playerCases.case == "case2" && playerCases.row == "row2") midleC++;
                if (playerCases.case == "case3" && playerCases.row == "row2") midleD++;
                if (playerCases.case == "case1" && playerCases.row == "row3") angleBG++;
                if (playerCases.case == "case2" && playerCases.row == "row3") midleB++;
                if (playerCases.case == "case3" && playerCases.row == "row3") angleBD++;
            }

            if (
                angleTG + midleT + angleTD == 3 ||
                midleG + midleC + midleD == 3 ||
                angleBG + midleB + angleBD == 3 ||
                angleTG + midleG + angleBG == 3 ||
                midleT + midleC + midleB == 3 ||
                angleTD + midleD + angleBD == 3 ||
                angleTG + midleC + angleBD == 3 ||
                angleTD + midleC + angleBG == 3
            ) {
                player.score++;
                this.party.state = false;
            }
        },
    },
};
</script>

<template>

<div class="scoreBoard" v-if="!party.state">
    <h2>Score :</h2> 
    {{ players.player1.name }} {{ players.player1.score }} / {{ players.player2.score }} {{ players.player2.name }}
</div>

    <table>
        <tr id="row1">
            <td id="case1" v-on:click="changeValue"></td>
            <td id="case2" v-on:click="changeValue"></td>
            <td id="case3" v-on:click="changeValue"></td>
        </tr>
        <tr id="row2">
            <td id="case1" v-on:click="changeValue"></td>
            <td id="case2" v-on:click="changeValue"></td>
            <td id="case3" v-on:click="changeValue"></td>
        </tr>
        <tr id="row3">
            <td id="case1" v-on:click="changeValue"></td>
            <td id="case2" v-on:click="changeValue"></td>
            <td id="case3" v-on:click="changeValue"></td>
        </tr>
    </table>

    <button class="playBtn" @click="newParty">nouvelle manche</button>
    <button class="playBtn" @click="initGame">nouvelle partie</button>
</template>

<style>
table {
    user-select: none;
    width: 500px;
    height: 500px;
}

td {
    cursor: pointer;
    text-align: center;
    max-width: 50px;
    max-height: 50px;
    width: 150px;
    height: 150px;
    font: bold 50px arial;
    padding: 0;
    background-color: #eaeaea2a;
    backdrop-filter: blur(20px);
}

.scoreBoard {
    width: fit-content;
    font: bold;
    padding: 10px;
    margin: 10px;
    border-radius: 5px;
    box-shadow: 0 0 0px 1px #0fa0d9;
    background-color: #eaeaea71;
    backdrop-filter: blur(20px);
}
</style>