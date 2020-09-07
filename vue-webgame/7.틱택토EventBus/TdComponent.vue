 <template>
    <td @click="onClickTd">{{cellData}}</td>
</template>

<script>
    import EventBus from './EventBus';
    export default {
        props: {
            cellData: String,
            rowIndex: Number,
            cellIndex: Number,
        },
        methods: {
            onClickTd() {
                if(this.cellData) return;           //누른 칸을 또 눌렀을 경우
                EventBus.$emit('clickTd', this.rowIndex, this.cellIndex);
            },
        }
    };
</script>