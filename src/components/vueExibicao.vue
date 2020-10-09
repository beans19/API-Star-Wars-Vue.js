<template>
  <!--Inicio de código com caixa de pesquisa e cards-->
  <div class="divMaster">

    <div class="header">
      <h1>Framework <font>Vue.js</font> - API Star Wars</h1>
    </div>

    <!--Caixa de Pesquisa-->
    <div class="searchCharacter">
      <div class="searchEsquerda">
          <p>Search for a character:</p>
      </div>
      <div class="searchDireita">
        <input id="pesquisa" type="text" class="inputSearch">
        <button id="btn" v-on:click="pesquisarPersonagens()" class="btnSearch"><i></i></button>
      </div>
    </div>
          
    <!--Exibição de Personagens-->
    <div v-for="personagem in grupoPersonagens" :key="personagem.name">
      <div class="containerItem">
        <div class="card">
          <div class="title">
            <div class="sliderTitle">
              <h3>{{personagem.name}}</h3>
            </div>
          </div>

          <!--Card do Personagem-->
          <div class="flip-card">
            <div class="flip-card-inner">

              <!--Card - Parte da Frente-->
              <div class="flip-card-front">
                <div class="sliderBody">
                  <img v-bind:src="`https://starwars-visualguide.com/assets/img/characters/${personagem.url.replace(/[^0-9 ]/g,'')}.jpg`"/>
                </div>
              </div>

              <!--Card - Parte de Trás-->
              <div class="flip-card-back">
                <div class="back-header">
                  <h2>{{personagem.name}}</h2>
                </div>
                <div class="back-footer">
                  <p>Height: {{personagem.height}}</p>
                  <p>Birth Year: {{personagem.birth_year}} </p> 
                  <p>Hair Color: {{personagem.hair_color}}</p>
                  <p>Eye Color: {{personagem.eye_color}}</p>
                  <p>Mass: {{personagem.mass}}</p>
                  <p>Gender: {{personagem.gender}}</p>
                </div>
              </div>

             </div>
           </div>

         </div>
       </div>
     </div>
   </div>  
</template>

<script>
export default {
  name: 'vueExibicao',
  data: function(){
    return {
      grupoPersonagens: []
    }
  },
  methods: {

    listarPersonagens: function(nome){
      this.grupoPersonagens = [];
      const url = `https://swapi.co/api/people/?search=${nome}`;
            
      const sw = fetch(url)
                .then(response => response.json())
                .then(response => {
                    response.results.map(personagem => {
                        this.grupoPersonagens.push(personagem);
                    });
                });
    },

    pesquisarPersonagens: function(){
      let campo_pesquisa = document.querySelector("#pesquisa").value
      if(campo_pesquisa != ""){
        this.listarPersonagens(campo_pesquisa);
      }
    }
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
*{
  font-family: Verdana;
}

@media only screen and (max-device-width: 650px) {
  h1{
    font-size: 16px;
  }

  p{
    font-size: 12px;
  }
  .searchEsquerda{
    width: 60%;
  }

  .searchEsquerda p{
    margin-left: 50px;
  }
  .searchDireita{
    width: 40%;
  }

  .header{
    width: 100%;
  }
}

.divMaster{
  width: 100%;
  height: auto;
}

.header{
    background-color: #000000;
    width: 50%;
    height: 100px;
    padding-top: 1%;
    text-align: center;
    margin-left: 24%;
    font-family: Verdana;
    color: #ffffff;
    border-radius: 10px;
    box-shadow: 1px 1px 10px #000000;
    text-shadow: 1px 1px 10px #000000;
}

h1 font{
  color: #00bd55;
}

.searchCharacter{
    width: 100%;
    height: 80px;
    margin-top: 4%;
    font-family: Verdana;
    color: #ffffff;
    font-size: 14px;
}

.searchCharacter label{
  margin-left: auto;
  margin-top: 0.8%;
  margin-right: 1%;
  float: left;
}

.searchEsquerda{
  width: 40%;
  height: 100%;
  text-align: right;
  float: left;
}

.searchEsquerda p{
  margin-right: 10px;
}

.searchDireita{
  width: 60%;
  height: 100%;
  float: left;
}

.inputSearch{
    width: 45%;
    height: 25px;
    margin-top: 7px;
    float: left;
}

.btnSearch{
    width: 30px;
    height: 30px;
    display: block;
    float: left;
    margin-top: 8px;
    margin-left: 10px;
    border-radius: 50px;
    border: none;
    cursor: pointer;
    background-color: #ffffff;
}

button:focus {outline:0;}

.btnSearch i{
    width: 20px;
    height: 20px;
    background-image: url(../img/searchIcon.png);
    background-size: contain;
    background-repeat: no-repeat;
    float: left;
}

.btnSearch:hover{
    background-color: rgb(187, 187, 187);
}

.item{
    width: 15%;
    height: 400px;
    float: left;
    margin-right: 20px;
    margin-left: 40px;
    margin-top: 30px;
}

.sliderTitle{
    width: 100%;
    height: 30px;
    margin-left: auto;
    margin-right: auto;
    font-family: verdana;
    color: #ffffff;
}

.sliderBody{
    width: 250px;
    height: 350px;
}

.sliderBody img{
    width: inherit;
    height: inherit;
}

.card{
  width: 250px;
  height: 350px;
  margin-top: 90px;
  margin-left: 70px;
  float: left;
}

.title{
  text-align: center;
  margin: 40px auto 30px;
}

.flip-card{
  width: 250px;
  height: 350px;
  margin: auto;
  cursor: pointer;
}

.flip-card-back{
  background-color: #000000;
  color: #ffffff;
  transform: rotateY(180deg);
  z-index: 1;
}

.flip-card-back .back-header{
  height: 45%;
  text-align: center;
}

.flip-card-back .back-header img{
  width: 50%;
  margin-top: 20px;
}

.flip-card-inner{
  position: relative;
  height: 100%;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.flip-card-back, .flip-card-front{
  position: absolute;
  width: 100%;
  height: 100%;
}

.flip-card:hover .flip-card-inner{
  transform: rotateY(180deg);
  backface-visibility: hidden;
}
.flip-card-back .back-footer{
  height: 48%;
  padding: 0 15px;
}

.back-footer p{
  text-align: left;
  margin: 2px;
  padding: 0;
}

</style>