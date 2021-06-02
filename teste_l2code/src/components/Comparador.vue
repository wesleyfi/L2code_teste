<template>  
        <div>
            <p class="aviso" v-show="alert_value">{{msg_alert}}</p>
            <div id="raiz">
                <h1>Comparador de distância de lojas</h1>
                <br>
                <div class="input">
                    <div>
                        <label for="n_lojas">Número de lojas a serem visitadas</label>
                        <input type="text" v-model="stores_number" name="n_lojas" placeholder="ex: 4"> 
                    </div>
                    <p class="aviso soft">O número máximo de lojas é 20, logo só serão<br> aceitos valores de 1 até 20</p>
                    <br>
                    <div>
                        <label for="posicoes">Posições das lojas</label>
                        <input type="text" v-model="stores_position" name="n_lojas" placeholder="ex: 5 10 48 95">  
                    </div>
                    <p class="aviso soft">As posições vão de 0 até 99 <br>e os valores deverão estar separados por espaços</p>
                    <br>
                <button v-on:click="calcular()">Calcular</button>
                </div>       
                <h2>RESULTADO: {{resutado_value}}</h2>
            </div>
           
        </div>
        
                                
                
</template>

<script>
export default {
  name: 'Comparador',
  props: {

  },
  data(){
      return{
          stores_number:"",
          stores_position:"",
          resutado_value:"",
          alert_value:false,
          msg_alert:""

      }
  },
  methods: {
      calcular(){
            
        this.stores_number = parseInt(this.stores_number)  
        //pegando o valor do campo e atribuindo a uma string
          var position = this.stores_position.toString()
        //usando a função split para separar os valores
          var re =  /\s+/
          let allPosition = position.split(re)
          
        //transformando o array em um array de inteiros
          let positionsInt = allPosition.map((item)=>{

              if(item!=""&&item!=" "&&!item.isNaN){

                   return parseInt(item)

              }else{
                  //caso ocorra um espaço indesejado no input é retornado "s" para ser tratado a frente
                  return "s"
              }
             
          })
          
          //removendo os itens indesejados caso ocorram
          positionsInt.forEach((item, indice, array) => {
              if(item=="s"){
                  array.splice(indice);
              }
              
          })
        

        //colcando os números em ordem crescente
          positionsInt = positionsInt.sort((a,b)=> a-b)
         

        //atribuindo o resultado
            let result = 0
            positionsInt.forEach((item, indice, array) => {

                if(indice!=0){
                result = result + (item - array[indice-1])                  
                }

            })

        //tratando os erros 

                 
          if(this.stores_number!=positionsInt.length){

              this.alert_value = true
              this.msg_alert = "O numero de lojas e de posições não correspondem"
              console.log(positionsInt)

          }else{

              this.alert_value =false

          }
          if(this.stores_number>20){

              this.alert_value = true
              this.msg_alert = "Numero de lojas inválido"

          }
          if(this.stores_number.isNaN){

              this.alert_value = true
              this.msg_alert = "campos vazios ou caracteres inválidos"
              
          } 
          
          if(!this.alert_value){

               this.resutado_value = result*2

          }else{

              this.resutado_value= "ocorreu um erro"

          }
            
            
        }
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    #raiz{
        background-color: rgb(206, 206, 206);
        padding: 2px 15px 5px 15px;      
        border-radius: 15px;
        width: max-content;  
    }
    *{
    }
    .input{
        display: flex;
        flex-direction: column;
        
    }
    .input *{
        margin: 5px;
   }
    .input button {
        color:white;
        width: min-content;
        font-size: 1.5rem;
        background-color: rgb(65, 214, 78);
        border: none;
        align-self: center;
        padding: 5px;
        border-radius: 5px;
        cursor: pointer;

    }
    .input button:hover{
        background-color: rgb(104, 231, 115);
    }
    .input label{
        font-size: 1.3rem;
    }
    .input input[type = text] {
        border: none;
        height: 1.3rem;
    }
   
    .aviso{
        color: rgb(255, 255, 255);
        font-size: 1.3rem;
        text-align: center;
        background-color: tomato;
        padding: 10px;
        
    }
    .soft{
        background-color:rgb(243, 164, 150) ;
        color: rgb(56, 56, 56);
    }
    h1{
        text-align: center;
        
    }
    h2{
        background-color: white;
        padding: 10px;
        text-align: center;
    }
</style>
