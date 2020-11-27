<template>
    <div>
        <div
            class="mb-4"
            :class="{ 'd-none': isHistory }"
            v-for="(h, i) in history"
            :key="i"
        >
            <div class=" history">{{ h }}</div>
        </div>
        <div class="calculator">
            <div class="display">{{ current || "0" }}</div>
            <div @click="clear()" class="btn operator">C</div>
            <div @click="append('<<<')" class="btn operator">{{ "<<<" }}</div>
            <div @click="append('/')" class="btn operator">%</div>
            <div @click="append('/')" class="btn operator">/</div>
            <div @click="append('7')" class="btn">7</div>
            <div @click="append('8')" class="btn">8</div>
            <div @click="append('9')" class="btn">9</div>
            <div @click="append('*')" class="btn operator">x</div>
            <div @click="append('4')" class="btn">4</div>
            <div @click="append('5')" class="btn">5</div>
            <div @click="append('6')" class="btn">6</div>
            <div @click="append('-')" class="btn operator">-</div>
            <div @click="append('1')" class="btn">1</div>
            <div @click="append('2')" class="btn">2</div>
            <div @click="append('3')" class="btn">3</div>
            <div @click="append('+')" class="btn operator">+</div>
            <div @click="showHistory()" class="btn operator">H</div>
            <div @click="append('0')" class="btn">0</div>
            <div @click="append('.')" class="btn">.</div>
            <div @click="sum()" class="btn operator">=</div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            current: "",
            total: "",
            history: [],
            isHistory: true,
            localStorageData: "",
        };
    },
    methods: {
        clear() {
            this.current = "";
        },
        append(number) {
            this.current = `${this.current}${number}`;
        },
        sum() {
            this.total = eval(this.current);
            this.history.push(`${this.current} = ${this.total}`);
            this.current = this.total;

            // todo : check if already have vue-calculator
            if (localStorage.getItem("vue-calculator") === null) {
                localStorage.setItem(
                    "vue-calculator",
                    JSON.stringify(this.history)
                );
            } else {
                // todo : push new history
                this.localStorageData = JSON.parse(
                    localStorage.getItem("vue-calculator")
                );
                this.localStorageData.push(this.current);
                console.log(this.localStorageData);
                localStorage.setItem(
                    "vue-calculator",
                    JSON.stringify(this.localStorageData)
                );
            }
        },
        showHistory() {
            this.isHistory == false
                ? (this.isHistory = true)
                : (this.isHistory = false);
        },
    },
};
</script>

<style scoped>
.mb-4 {
    margin-bottom: 40px;
}

.d-none {
    display: none;
}

.history {
    font-size: 50px;
    color: #42b983;
}

.calculator {
    width: 400px;
    height: 600px;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
}

.display {
    margin-bottom: 10px;
    grid-column: 1 / 5;
    background-color: #333;
    color: white;
    display: flex;
    align-items: center;
    justify-content: space-around;
    border-radius: 5px;
}
.zero {
    grid-column: 1 / 3;
}
.btn {
    background-color: #adcabd;
    border: 1px solid #f2f2f2;
    border-radius: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    transition: 0.3s;
}

.btn:hover {
    background-color: #6d9e88;
}

.operator {
    background-color: #42b983;
    color: white;
}

.operator:hover {
    background-color: #42c58a !important;
}
</style>
