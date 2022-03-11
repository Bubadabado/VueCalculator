<template>
    <div class="calculator">
        <div class="result-screen">
            <p>{{result}}</p>
        </div>
        <div class="calculator-button-container">
            <div v-for="button in buttonList" :key="button.id">
                <button v-bind:class="{ calculatorButtonColor: isNaN(button.name), calculatorButtonWide: (button.name == 0 || button.name == 'AC' || button.name == '=')}" class="calculator-button-bg" v-on:click="buttonPressed(button)">{{ button.name }}</button>
            </div> 
        </div>
    </div>
</template>

<script>

export default {
    name: "CalculatorComp",
    props: {
        history: Array
    },
    data() {
        return { 
            value: "0",
            previousValue: 0,
            previousOperation: "",
            buttonList: [{name: "AC"}, {name: "="}, {name: "1"}, {name: "2"}, {name: "3"}, {name: "+"}, {name: "4"}, {name: "5"}, {name: "6"}, {name: "-"}, {name: "7"}, {name: "8"}, {name: "9"}, {name: "*"}, {name: "0"}, {name: "."}, {name: "/"}]
        }
    },
    computed: {
        result() {
            return this.$data.value;
        }
    },
    methods: {
        buttonPressed(button) {
            const MAX_INPUT_DIGITS = 10; //arbitrarily supports 10 digits
            if(!isNaN(button.name)) //it is a number
            {
                if((isNaN(this.$data.value)) || this.$data.value == "0")
                {
                    this.$data.value = button.name;
                }
                else if(this.$data.value.length < MAX_INPUT_DIGITS)
                {
                    this.$data.value += button.name;
                }
            }
            else if(button.name == "AC") //clear
            {
                this.$data.value = "0";
                this.$root.$data.history.push("clear");
            }
            else if(button.name == ".") //decimal
            {
                if(!this.$data.value.includes(".") && this.$data.value.length < MAX_INPUT_DIGITS)
                {
                    if(isNaN(this.$data.value))
                    {
                        this.$data.value = "0" + button.name;
                    }
                    else
                    {
                        this.$data.value += button.name;
                    }
                }
            }
            else if(button.name == "=") //compute the previous stored value with the current value based on the previous operator
            {
                if(!isNaN(this.$data.value) && this.$data.previousOperation != "")
                {
                    var temp = this.$data.value;
                    if(this.$data.previousOperation == "+")
                    {
                        this.$data.value = "" + (parseFloat(this.$data.previousValue) + parseFloat(this.$data.value));
                        this.$root.$data.history.push(this.$data.previousValue + " + " + temp + " = " + this.$data.value);
                    }
                    else if(this.$data.previousOperation == "-")
                    {
                        this.$data.value = "" + (parseFloat(this.$data.previousValue) - parseFloat(this.$data.value));
                        this.$root.$data.history.push(this.$data.previousValue + " - " + temp + " = " + this.$data.value);
                    }
                    else if(this.$data.previousOperation == "*")
                    {
                        this.$data.value = "" + (parseFloat(this.$data.previousValue) * parseFloat(this.$data.value));
                        this.$root.$data.history.push(this.$data.previousValue + " * " + temp + " = " + this.$data.value);
                    }
                    else if(this.$data.previousOperation == "/")
                    {
                        this.$data.value = "" + (parseFloat(this.$data.previousValue) / parseFloat(this.$data.value));
                        this.$root.$data.history.push(this.$data.previousValue + " / " + temp + " = " + this.$data.value);
                    }

                    this.$data.previousValue = this.$data.value;
                    this.$data.previousOperation = "";
                }
            }
            else //it is an operator
            {
                if(!isNaN(this.$data.value))
                {
                    this.$data.previousValue = this.$data.value;
                    console.log("previous value " + this.$data.previousValue);
                }
                this.$data.previousOperation = button.name;
                this.$data.value = button.name;
            }
            console.log(button.name);
            console.log("History: " + this.$root.$data.history);
        }
    }
}
</script>


<style scoped>
.calculator {
    background-color: rgb(36, 36, 36);
    color: white;
    width: 500px;
    padding-top: 26px;
    padding-bottom: 26px;
    margin-left: auto;
    margin-right: auto;
    border-radius: 8px;
}
.calculator-button-container {
    /* columns: 4; */
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
}
.calculator-button-bg {
    background-color: rgb(77, 77, 77);
    color: white;
    flex-basis: 100%; 
    width: 100px;
    height: 100px;
    padding: 10px;
    text-align: center;
    vertical-align: middle;
    border-radius: 8px;
    border-width: 2px;
    border-color: rgb(56, 52, 61);
}
.calculatorButtonWide {
    width: 210px;
}
.calculatorButtonColor {
    background-color: rgb(66, 49, 114);
}
.result-screen {
    width: 80%;
    margin: 10px;
    margin-left: auto;
    margin-right: auto;
    padding: 16px;
    border-radius: 8px;
    text-align: right;
    background-color: rgb(0, 0, 0);
}
</style>
