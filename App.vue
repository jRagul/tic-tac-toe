<template>
    <div class="mega" style="font-size: 70px;">Tic Tac Toe</div>
    <div class="mega">
        <div class="major">
            <div @click="zemn(1)" class="minor" :class="{ 'disabled': disabled[0]}" :id='color[0]' > {{ textesh[0] }} </div>
            <div @click="zemn(2)" class="minor" :class="{ 'disabled': disabled[1]}" :id='color[1]'> {{ textesh[1] }} </div>
            <div @click="zemn(3)" class="minor" :class="{ 'disabled': disabled[2]}" :id='color[2]'> {{ textesh[2] }} </div>
            <div @click="zemn(4)" class="minor" :class="{ 'disabled': disabled[3]}" :id='color[3]'> {{ textesh[3] }} </div>
            <div @click="zemn(5)" class="minor" :class="{ 'disabled': disabled[4]}" :id='color[4]'> {{ textesh[4] }} </div>
            <div @click="zemn(6)" class="minor" :class="{ 'disabled': disabled[5]}" :id='color[5]'> {{ textesh[5] }} </div>
            <div @click="zemn(7)" class="minor" :class="{ 'disabled': disabled[6]}" :id='color[6]'> {{ textesh[6] }} </div>
            <div @click="zemn(8)" class="minor" :class="{ 'disabled': disabled[7]}" :id='color[7]'> {{ textesh[7] }} </div>
            <div @click="zemn(9)" class="minor" :class="{ 'disabled': disabled[8]}" :id='color[8]'> {{ textesh[8] }} </div>
        </div>
        
    </div>
    <div class="mega" style="margin-top: 20px; font-size: 40px;">
        {{ result }}
    </div>
    <div class="mega">
        <button @click="reset" class>Reset</button>
    </div>
    
</template>

<script>
    export default{
        methods:{
            zemn(id){
                if(this.state == true){
                    this.textesh[id-1] = 'X'
                    this.state = false
                    this.counter += 1
                    this.color[id-1] = "red"
                    this.result = "O's Turn"
                }
                else{
                    this.textesh[id - 1] = 'O'
                    this.state = true
                    this.counter += 1
                    this.color[id-1] = "blue"
                    this.result = "X's turn"
                }
                this.disabled[id - 1] = true;
                this.winnerCheck()
            },
            winnerCheck(){
                let i;
                for(i=0;i<this.winCondition.length;i++){
                    const cond = this.winCondition[i]
                    let BoxA = this.textesh[cond[0]]
                    let BoxB = this.textesh[cond[1]]
                    let BoxC = this.textesh[cond[2]]
                    
                    
                    if(BoxA === ""||BoxB === "" || BoxC === ""){
                        continue;
                    }
                    if(BoxA === BoxB && BoxB === BoxC){
                        this.winnesh = true
                        this.resultesh(BoxA)
                        break;
                    }
                    if(this.counter == 9){
                        this.resultesh("draw")
                    }
                    
                }
            },
            resultesh(res){
                if( res == "draw"){
                    this.result = "Draw"
                }
                else{
                    this.result = res + " Won"
                }
            },
            colorChange(){
                if(this.state == true){
                    return "red"
                }
                else if(this.state == false){
                    return "blue"
                }
            },
            reset(){
                window.location.reload()
            }
            
            
        },
        data(){
            return{
                state:true,
                textesh:["","","","","","","","",""],
                winCondition:[[0,1,2],[0,4,8],[0,3,6],[1,4,7],[2,5,8],[3,4,5],[6,7,8],[2,4,6]],
                winnesh:false,
                counter:0,
                result:'',
                disabled: [false, false, false, false, false, false, false, false, false],
                color : []
            }
        }
    }
    
</script>

<style>
    .major{
        margin-left: -100px;
        display: grid;
        
        grid-template-columns: 1fr 1fr 1fr;
        width: 150px;
    }
    .minor{
        display: flex;
        border:solid black 2px;
        width: 50px;
        height:50px;
        padding: 10px;
        justify-content:center;
        align-items:center;
        font-size: 40px;
        transition: 0.2s;
    }
    .mega{
        margin: 0px;
        display: flex;
        justify-content: center;
        flex-direction: row;
    }
    .disabled {
        pointer-events: none; /* Disable pointer events to make the element unclickable */
         /* Optionally reduce opacity to indicate the disabled state */
    }
    #red{
        color: rgb(201, 35, 104);
    }
    #blue{
        color:rgb(88, 184, 223);
    }
    button{
        padding: 10px 50px;
        border-radius: 20px;
        box-shadow: 1px 6px rgba(0, 0, 0, 0.753);
        transition: 0.3s;
    }
    button:active{
        margin-top: 6px;
        box-shadow: none;
    }
    .minor:active{
        background-color: rgb(45, 56, 117);
    }
</style>