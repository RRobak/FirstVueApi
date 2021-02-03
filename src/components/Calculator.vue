<template>
  <div class="calculator">
        <table class="numbers">
            <tr>
                <td colspan="3">
                    <output id="Eq"></output>
                </td>
                <td rowspan="2">
                    <button type="AC" class="ope" v-on:click="setzerotooutput()">AC</button>
                </td>
            </tr>
            <tr>
                <td colspan="3">
                    <output id="pole">Numbers</output>
                </td>
            </tr>
            <tr>
                <td>
                    <button type="7" v-on:click="display(7)">7</button>
                </td>
                <td>
                    <button type="8" v-on:click="display(8)">8</button>
                </td>
                <td>
                    <button type="9" v-on:click="display(9)">9</button>
                </td>
                <td>
                    <button type="/" class="ope" v-on:click="math('/') ">/</button>
                </td>
            </tr>
            <tr>
                <td>
                    <button type=" 4 " v-on:click="display(4) ">4</button>
                </td>
                <td>
                    <button type="5 " v-on:click="display(5) ">5</button>
                </td>
                <td>
                    <button type="6 " v-on:click="display(6) ">6</button>
                </td>
                <td>
                    <button type="* " class="ope" v-on:click="math('*') ">*</button>
                </td>
            </tr>
            <tr>
                <td>
                    <button type="1 " v-on:click="display(1) ">1</button>
                </td>
                <td>
                    <button type="2 " v-on:click="display(2) ">2</button>
                </td>
                <td>
                    <button type="3 " v-on:click="display(3) ">3</button>
                </td>
                <td>
                    <button type="- " class="ope" v-on:click="math('-') ">-</button>
                </td>
            </tr>
            <tr>
                <td>
                    <button type="0 " v-on:click="display(0) ">0</button>
                </td>
                <td>
                    <button type=", ">,</button>
                </td>
                <td>
                    <button type="=" class="ope" v-on:click="resum() ">=</button>
                </td>
                <td>
                    <button type="+ " class="ope" v-on:click="math('+') ">+</button>
                </td>
            </tr>
</table>
    </div>
</template>

<script>
export default{
    name: 'App',
   
data(){
    return{
    x:0,
    tmp : 0,
    equation : "+",
    upperpole : "",
    mathresult : 0,
    value:0
    }
},
methods: {
    display(a) {
    this.x = (10 * this.x) + a;
    document.getElementById("pole").innerHTML = this.x;
},
math(a) {
    this.tmp = this.x;
    switch (this.equation) {
        case '/':
            this.mathresult /= this.x;
            break;
        case '*':
            this.mathresult *= this.x;
            break;
        case '-':
            this.mathresult -= this.x;
            break;
        case '+':
            this.mathresult += this.x;
            break;
        default:
            document.getElementById("pole").innerHTML = 'ERROR';
    }
    this.equation = a;
    this.x = 0;
    if (this.tmp != 0)
        this.upperpole = this.upperpole + this.tmp + this.equation;
    else
        this.upperpole += this.equation;

    document.getElementById("Eq").innerHTML = this.upperpole;

},
resum() {
    this.value = parseInt(document.getElementById("pole").value);
    switch (this.equation) {
        case '/':
            this.mathresult /= this.value;
            document.getElementById("pole").innerHTML = this.mathresult;
            break;
        case '*':
           this.mathresult *= this.value;
            document.getElementById("pole").innerHTML = this.mathresult;
            break;
        case '-':
            this.mathresult -= this.value;
            document.getElementById("pole").innerHTML = this.mathresult;
            break;
        case '+':
            this.mathresult += this.value;
            document.getElementById("pole").innerHTML = this.mathresult;
            break;
        default:
            document.getElementById("pole").innerHTML = 'ERROR';
    }
    this.tmp = 0;
    this.x = 0;
    this.equation = '+';
    document.getElementById("Eq").innerHTML = this.upperpole + this.value + '=' + this.mathresult;
    this.upperpole = document.getElementById("pole").value;
},
setzerotooutput() {
    this.x = 0;
    this.tmp = 0;
    this.equation = "+";
    this.upperpole = "";
    this.mathresult = 0;
    document.getElementById("pole").innerHTML = 0;
    document.getElementById("Eq").innerHTML = "";
},
}
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border: 3px solid darkblue;
    padding: 10px;
}

.numbers {
    border: 1px solid blue;
}

button {
    width: 40px;
    height: 40px;
}

.ope {
    background-color: purple;
    border: none;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 22px;
    transition-duration: 0.4s;
}

.ope:hover {
    background-color: purple;
    color: white;
    border-radius: 12px;
}
</style>
