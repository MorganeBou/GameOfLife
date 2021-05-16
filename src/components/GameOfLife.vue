<template>
    <div>
        <button v-on:click="goToTheNextMatrix">Avancer  dans le cycle</button>
        <button v-on:click="play">Play</button>
        <button v-on:click="stopTheMatrix">Stopper</button>
        <table v-on:mouseup="stopChangeState" >
            <tr v-for="(line,lineNumber) in currentMatrix"
                :key="line.index"
                :lineNumber="line.index"
            >
                <td v-for="(cell, colNumber) in line"
                    :key="cell.index"
                    :colNumber="cell.index"
                    :style="{ backgroundColor:getColor(cell),height:'5px',width:'5px' }"
                    :test="cell.index"

                v-on:mousedown="changeStateMouseDown(colNumber, lineNumber)"
                v-on:mouseover="changeStateByMove(colNumber, lineNumber)">

                </td>
            </tr>
        </table>
        {{mouseDowned}}
    </div>

</template>

<script>
    export default {
        name: 'GameOfLife',
        data: function () {
            return {
                currentMatrix: [],
                monInterval:{},
                mouseDowned: false,
            }
        },
        mounted: function () {
            let nextMatrix = []

            for (let y = 0; y <= 50; y++) {
                nextMatrix [y] = []
                for (let x = 0; x <= 50; x++) {
                    nextMatrix [y][x] = false
                }
            }
            nextMatrix[25][25] = true
            nextMatrix[25][23] = true
            nextMatrix[25][22] = true
            nextMatrix[23][25] = true
            nextMatrix[22][25] = true
            nextMatrix[21][25] = true
            nextMatrix[24][25] = true
            nextMatrix[26][25] = true
            nextMatrix[25][24] = true
            nextMatrix[25][23] = true
            nextMatrix[27][25] = true
            nextMatrix[25][21] = true
            nextMatrix[25][20] = true
            nextMatrix[28][25] = true
            nextMatrix[29][25] = true
            nextMatrix[25][26] = true
            nextMatrix[25][27] = true
            nextMatrix[25][28] = true
            nextMatrix[25][29] = true
            nextMatrix[25][30] = true


            this.currentMatrix = nextMatrix

        },
        methods: {
            getColor(cell) {
                if (cell == true) {
                    return "black"
                } else {
                    return "#eee"
                }
            },
            changeStateMouseDown(col, row){
               this.mouseDowned= true
                console.log(col, row)
                console.log("1- test mouseDown"+ this.currentMatrix [row][col]+ "mouse downed"+ this.mouseDowned)

                this.inverseCellState(col, row)
            },
            changeStateByMove(col, row){

                if(this.mouseDowned==true){
                    console.log(col, row)
                    console.log("2 - test du mouseMove")

                    this.inverseCellState(col, row)
                }
            },
            inverseCellState(col, row){
              this.$set (this.currentMatrix [row],col, !this.currentMatrix [row][col])
            },
            stopChangeState(){
                console.log("3 - stop")
                this.mouseDowned= false
            },

            play(){
                this.monInterval = setInterval(this.goToTheNextMatrix, 200)
            },

            stopTheMatrix(){
                clearInterval(this.monInterval)
            },
            goToTheNextMatrix() {
                console.log(this.currentMatrix)
                let newMatrix = []
                for (let y = 0; y <= 50; y++) {
                    newMatrix [y] = []
                    for (let x = 0; x <= 50; x++) {
                        if (this.currentMatrix[y][x] == true) {
                            // compter les cases voisines vivantes
                            // if ([y - 1] !== undefined && (y + 1) !== undefined && (x + 1) !== undefined && (x - 1) !== undefined) {
                            let counterNeighbour = 0

                            if (typeof this.currentMatrix[y - 1] !== 'undefined' && typeof this.currentMatrix[y - 1][x] !== 'undefined' && this.currentMatrix[y - 1][x] == true) {
                                counterNeighbour++
                                console.log(counterNeighbour)
                            }
                            if (typeof this.currentMatrix[y + 1] !== 'undefined' && typeof this.currentMatrix[y + 1][x] !== 'undefined' && this.currentMatrix[y + 1][x] == true) {
                                counterNeighbour++
                            }
                            if (typeof this.currentMatrix[y] !== 'undefined' && typeof this.currentMatrix[y][x - 1] !== 'undefined' && this.currentMatrix[y][x - 1] == true) {
                                counterNeighbour++
                            }
                            if (typeof this.currentMatrix[y] !== 'undefined' && typeof this.currentMatrix[y][x + 1] !== 'undefined' && this.currentMatrix[y][x + 1] == true) {
                                counterNeighbour++
                            }
                            if (typeof this.currentMatrix[y - 1] !== 'undefined' && typeof this.currentMatrix[y - 1][x + 1] !== 'undefined' && this.currentMatrix[y - 1][x + 1] == true) {
                                counterNeighbour++
                            }
                            if (typeof this.currentMatrix[y + 1] !== 'undefined' && typeof this.currentMatrix[y + 1][x + 1] !== 'undefined' && this.currentMatrix[y + 1][x + 1] == true) {
                                counterNeighbour++
                            }
                            if (typeof this.currentMatrix[y - 1] !== 'undefined' && typeof this.currentMatrix[y - 1][x - 1] !== 'undefined' && this.currentMatrix[y - 1][x - 1] == true) {
                                counterNeighbour++
                            }
                            if (typeof this.currentMatrix[y + 1] !== 'undefined' && typeof this.currentMatrix[y + 1][x - 1] !== 'undefined' && this.currentMatrix[y + 1][x - 1] == true) {
                                counterNeighbour++
                            }
                            console.table([x,y,counterNeighbour])

                            if (counterNeighbour == 2 || counterNeighbour == 3) {
                                newMatrix[y][x] = true
                            } else {
                                newMatrix[y][x] = false
                            }

                        } else if (this.currentMatrix[y][x] == false) {
                            let counterNeighbour = 0

                            if (typeof this.currentMatrix[y - 1] !== 'undefined' && typeof this.currentMatrix[y - 1][x] !== 'undefined' && this.currentMatrix[y - 1][x] == true) {
                                counterNeighbour++
                                console.log(counterNeighbour)
                            }
                            if (typeof this.currentMatrix[y + 1] !== 'undefined' && typeof this.currentMatrix[y + 1][x] !== 'undefined' && this.currentMatrix[y + 1][x] == true) {
                                counterNeighbour++
                            }
                            if (typeof this.currentMatrix[y] !== 'undefined' && typeof this.currentMatrix[y][x - 1] !== 'undefined' && this.currentMatrix[y][x - 1] == true) {
                                counterNeighbour++
                            }
                            if (typeof this.currentMatrix[y] !== 'undefined' && typeof this.currentMatrix[y][x + 1] !== 'undefined' && this.currentMatrix[y][x + 1] == true) {
                                counterNeighbour++
                            }
                            if (typeof this.currentMatrix[y - 1] !== 'undefined' && typeof this.currentMatrix[y - 1][x + 1] !== 'undefined' && this.currentMatrix[y - 1][x + 1] == true) {
                                counterNeighbour++
                            }
                            if (typeof this.currentMatrix[y + 1] !== 'undefined' && typeof this.currentMatrix[y + 1][x + 1] !== 'undefined' && this.currentMatrix[y + 1][x + 1] == true) {
                                counterNeighbour++
                            }
                            if (typeof this.currentMatrix[y - 1] !== 'undefined' && typeof this.currentMatrix[y - 1][x - 1] !== 'undefined' && this.currentMatrix[y - 1][x - 1] == true) {
                                counterNeighbour++
                            }
                            if (typeof this.currentMatrix[y + 1] !== 'undefined' && typeof this.currentMatrix[y + 1][x - 1] !== 'undefined' && this.currentMatrix[y + 1][x - 1] == true) {
                                counterNeighbour++
                                console.log(counterNeighbour)
                            }
                            if (counterNeighbour == 3) {
                                newMatrix[y][x] = true
                            } else {
                                newMatrix[y][x] = false
                            }
                        }
                    }
                }

                this.currentMatrix = newMatrix

            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    table {
        border-spacing: 0px;
        border-collapse: separate;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
