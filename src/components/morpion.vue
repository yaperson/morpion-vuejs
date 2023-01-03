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
                    cases: []
                },
                player2: {
                    id: 1,
                    name: "player2",
                    score: 0,
                    isPlay: true,
                    cases: []
                }
            },
            party: {
                state: true
            }
        }
    },

    methods: {
        // set players scores and party state for start or restart party
        initGame() {
            window.location.reload()
        },

        newParty() {
            this.party.state = true
        },

        // Action when user play
        changeValue(event) {
            let targetId = event.currentTarget.id
            let row = event.currentTarget.parentNode
            let player1 = this.players.player1
            let player2 = this.players.player2

            if (player1.isPlay == true) {
                if (!row.querySelector("#" + targetId).innerText) {
                    row.querySelector("#" + targetId).innerText = "X"
                    player1.cases.push(targetId)
                    this.changePlayer()
                    this.checkScore(player1, row)
                }
            }
            else {
                if (!row.querySelector("#" + targetId).innerText) {
                    row.querySelector("#" + targetId).innerText = "O"
                    player2.cases.push(targetId)
                    this.changePlayer()
                    this.checkScore(player2, row)
                }
            }
        },

        // Change player statut (isPlay?)
        changePlayer() {
            if (this.players.player1.isPlay == true) {
                this.players.player1.isPlay = false
                this.players.player2.isPlay = true
            } else {
                this.players.player1.isPlay = true
                this.players.player2.isPlay = false
            }
        },

        // Check score of last player
        checkScore(player, row) {
            let case1 = 0
            let case2 = 0
            let case3 = 0

            console.log(player)
            for (let elem in player.cases) {
                switch (player.cases[elem]) {
                    case 'case1': case1++
                        break;
                    case 'case2': case2++
                        break;
                    case 'case3': case3++
                        break;
                    default: console.log(`il semble y avoir un problème`);
                }
            }

            if (
                case1 == 3 || 
                case2 == 3 ||
                case3 == 3 
            ) player.score++

            if (case1 >= 1 || case2 >= 1 || case3 >= 1) {
                // TODO check if it's diagonal
            }
            switch(row) {
                case row.querySelector("#case1"):

                case row.querySelector("#case2"):
                
                case row.querySelector("#case3"):
            }
        }
    },

}
</script>

<template>
    <h1>MORPION</h1>
    <h2>Score : </h2>

    <div>{{ players.player1.name }} {{ players.player1.score }}</div>
    <div>{{ players.player2.name }} {{ players.player2.score }}</div>

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

    <button @click="newParty">nouvelle manche</button>
    <button @click="initGame">nouvelle partie</button>

</template>

<style>
table {
    width: 500px;
    height: 500px;
    border: solid red;
}

td {
    text-align: center;
    padding: 10px;
    box-shadow: 0 0 1px 0 blue;
    max-width: 20px;
    max-height: 20px;
    width: 20px;
    height: 20px;
}
</style>