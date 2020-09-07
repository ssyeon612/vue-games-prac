<template>
    <td @click="onClickTd">{{cellData}}</td>
</template>

<script>
    export default {
        props: {
            cellData: String,
            rowIndex: Number,
            cellIndex: Number,
        },
        methods: {
            onClickTd() {
                if(this.cellData) return;           //누른 칸을 또 눌렀을 경우
                const rootData = this.$root.$data;
                console.log(rootData);
                this.$set(rootData.tableData[this.rowIndex], this.cellIndex, rootData.turn);

                let win = false;
                if (rootData.tableData[this.rowIndex][0] === rootData.turn && rootData.tableData[this.rowIndex][1] === rootData.turn && rootData.tableData) {
                    win = true;
                }
                if (rootData.tableData[0][this.rowIndex] === rootData.turn && rootData.tableData[1][this.rowIndex] === rootData.turn && rootData.tableData) {
                    win = true;
                }
                if (rootData.tableData[0][0] === rootData.turn && rootData.tableData[1][1] === rootData.turn && rootData.tableData[2][2] === rootData.turn) {
                    win = true;
                }
                if (rootData.tableData[0][2] === rootData.turn && rootData.tableData[1][1] === rootData.turn && rootData.tableData[2][0] === rootDta.trun) {
                    win = true;
                }
                if (win) {            // 이긴 경우: 3줄 달성
                    rootData.winner = rootData.turn;
                    rootData.trun = 'O';
                    rootData.tableData = [['', '', ''], ['', '', ''], ['', '', '']];
                } else { // 무승부
                    let all = true;         //all이 true면 무승부라는 뜻
                    rootData.tableData.forEach((row) => {
                        row.forEach((cell) => {
                            if (!cell) {
                                all = false;
                            }
                        });
                    });
                    if (all) { //무승부
                        rootData.turn = 'O';
                        rootData.winner = '';
                        rootData.tableData = [['', '', ''], ['', '', ''], ['', '', '']];
                    } else {        // 게임이 아직 끝나기 전이라 턴을 바꿔준다
                        rootData.turn = this.$root.$data.turn === 'O' ? 'X' : 'O';
                    }
                }
            },
        }
    };
</script>