<template>
    <div>
    <button> <img src="../assets/trava.png" alt="cadeado travado"/>Iniciar jogo</button>
    <table id="tab">
        <tr>
            <td id="1" class="one"></td><td id="2" class="one"></td><td id="3" class="tres"></td>
        </tr>
        <tr>
            <td id="4" class="one"></td><td id="5" class="one"></td><td id="6" class="tres"></td>
        </tr>
        <tr>
            <td id="7" class="dois"></td><td id="8" class="dois"></td><td id="9"></td>
        </tr>
    </table>
    <div id="risco"></div>
    </div>
</template>
<script>
export default { 
    mounted() {        
            this.preparaInicioJogo();        
    },     
    data() {
            return {
                jogoAcabou : false,
                variavelAtual : ""
            }
    },
    methods:{        
        iniciaJogo:function(){
            let cel = document.querySelectorAll("td");
            cel.forEach(vlr =>{
                    vlr.addEventListener('click', e => {
                        console.log(e);
                        if (this.exibeMarcacao(vlr.id)=="O"){
                            document.getElementById(vlr.id).style.color = "red";
                        }else{
                            document.getElementById(vlr.id).style.color = "blue";
                        }                           
                        this.validaTermino();         
                    });
            });
        },       
        preparaInicioJogo:function(){
            let botao = document.querySelector("button");
            botao.addEventListener('click', e =>{  
            if (!this.jogoAcabou){
                console.log(e);
                this.iniciaJogo();
                let img = document.querySelector("img");
                img.src="src/assets/trava.png";
                botao.style.backgroundColor = "yellow";
                botao.innerHTML = '<img src="../assets/destrava.png" alt="cadeado travado"/>Reiniciar Jogo';
            }else{
                    this.reiniciarJogo();
                }
            });
        },
        exibeMarcacao:function(objeto){    
            if(document.getElementById(objeto).innerHTML ==""){

                if (!this.jogoAcabou){
                    if (this.variavelAtual == "" || this.variavelAtual=="O"){ 
                        let valor = document.getElementById(objeto);
                        valor.innerHTML = "X";                               
                        return this.variavelAtual = "X";
                    }else{   
                        let valor = document.getElementById(objeto);  
                        valor.innerHTML = "O";                   
                        return this.variavelAtual = "O";  
                    }   
                }else{
                    alert("Jogo acabou!");
                    return this.variavelAtual = "";
                }
            }        
        },
        validaTermino:function(){

            let aJogo =[];

            for(let i = 1; i < 10 ; i++){
                    aJogo[i]=document.getElementById(i).innerHTML;  
            }

            let dimH1 = (aJogo[1] == aJogo[2] && aJogo[1] == aJogo[3] && aJogo[1] !="");
            if(dimH1)this.propriedades(0,150,280);        
            
            let dimH2 = (aJogo[4] == aJogo[5] && aJogo[4] == aJogo[6] && aJogo[4] !="");
            if(dimH2)this.propriedades(0,330,280); 

            let dimH3 = (aJogo[7] == aJogo[8] && aJogo[7] == aJogo[9] && aJogo[7] !="");
            if(dimH3)this.propriedades(0,515,280); 

            let dimV1 = (aJogo[1] == aJogo[4] && aJogo[1] == aJogo[7] && aJogo[1] !="");    
            if(dimV1)this.propriedades(90,0,90);    
            
            let dimV2 = (aJogo[2] == aJogo[5] && aJogo[2] == aJogo[8] && aJogo[2] !="");
            if(dimV2)this.propriedades(90,0,272);   
            
            let dimV3 = (aJogo[3] == aJogo[6] && aJogo[3] == aJogo[9] && aJogo[3] !="");
            if(dimV3)this.propriedades(90,0,455); 

            let dimD1 = (aJogo[1] == aJogo[5] && aJogo[1] == aJogo[9] && aJogo[1] !="");
            if(dimD1)this.propriedades(45,335,0); 

            let dimD2 = (aJogo[3] == aJogo[5] && aJogo[3] == aJogo[7] && aJogo[3] !="");
            if(dimD2)this.propriedades(135,340,0);
                

        },
        propriedades:function(rotate, top, left ){    
            let objeto = document.getElementById("risco");
            objeto.style.display = "table";     
            objeto.style.transform="rotate("+rotate+"deg)";
            if(top != 0){
                objeto.style.top= top+"px";
            }
            if(left != 0){
                objeto.style.left= left+"px";
            }
            this.jogoAcabou = true;        
        },
        reiniciarJogo:function(){

            let td = document.querySelectorAll("td");
            let objeto = document.getElementById("risco");
            objeto.style.display = "none"; 
            td.forEach(vlr =>{
                vlr.innerHTML = "";
                document.getElementById(vlr.id).style.color = "black";
                this.jogoAcabou = false;
            });

        }        
        
    }
}

</script>
<style scoped>
    td{
        width: 180px;
        height: 180px;
        text-align: center;
        font-size: 100px;
    }

    table{
        position: relative;
        margin: auto;
    }

    .one{   
        border-bottom: 2px solid;
        border-right: 2px solid;   
    }

    .dois{   
        border-right: 2px solid;   
    }

    .tres{   
        border-bottom: 2px solid;   
    }

    #risco{

        border: 8px solid red;
        position: absolute;
        width: 800px;
        top: 300px;
        left: 280px;
        display: none;
    } 

    button{
        width: 110px;
        border-radius: 15px;
        font-weight: bolder;
    }
    
</style>