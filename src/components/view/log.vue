<template>
  <div>
    <!-- Inscription -->
    <div v-if="showModalSignUp" :class="{isActive}">
      <div class="log">
        <button class="close-icon" @click="showModalSignUp= false">
          <svg width="16px" height="16px" viewBox="0 0 16 16" version="1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns="http://www.w3.org/2000/svg">
            <defs>
              <path d="M0 0L16 0L16 16L0 16L0 0Z" id="path_1" />
              <clipPath id="mask_1">
                <use xlink:href="#path_1" />
              </clipPath>
            </defs>
            <g id="Delete-icon">
            <path d="M0 0L16 0L16 16L0 16L0 0Z" id="Background" fill="none" fill-rule="evenodd" stroke="none" />
            <g clip-path="url(#mask_1)">
              <path d="M2.75 2.04297L2.04297 2.75L2.39844 3.10156L7.29297 8L2.04297 13.25L2.75 13.957L8 8.70703L12.8945 13.6055L13.25 13.957L13.957 13.25L13.6055 12.8945L8.70703 8L13.957 2.75L13.25 2.04297L8 7.29297L3.10156 2.39844L2.75 2.04297Z" id="Shape" fill="#111111" stroke="none" />
            </g>
            </g>
          </svg>
        </button>
        <div class="formulaire">
          <form action="">
            <label for="name">
              Nom:
              <input type="text" name="" id="name" placeholder="nom">
            </label>
            <label for="mail">
              Email:
              <input type="email" name="" id="mail" placeholder="mouzx@y.com">
            </label>
            <label for="password">
              Mot de passe:
              <input type="password" name="" id="password" placeholder="mot de passe">
            </label>
            <div class="submit">
              <button type="submit"> Enregister</button>
            </div>
          </form>
        </div>
        <div class="description">
          <p>Vous avez déjà un compte? <span @click="openLinks">Incrivez-vous</span></p>
        </div>
      </div>
    </div>
    <!-- Connexion -->
    <div v-if="showModalSignIn" :class="{isActive}">
      <div class="log">
        <button class="close-icon" @click="showModalSignIn= false">
          <svg width="16px" height="16px" viewBox="0 0 16 16" version="1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns="http://www.w3.org/2000/svg">
            <defs>
              <path d="M0 0L16 0L16 16L0 16L0 0Z" id="path_1" />
              <clipPath id="mask_1">
                <use xlink:href="#path_1" />
              </clipPath>
            </defs>
            <g id="Delete-icon">
            <path d="M0 0L16 0L16 16L0 16L0 0Z" id="Background" fill="none" fill-rule="evenodd" stroke="none" />
            <g clip-path="url(#mask_1)">
              <path d="M2.75 2.04297L2.04297 2.75L2.39844 3.10156L7.29297 8L2.04297 13.25L2.75 13.957L8 8.70703L12.8945 13.6055L13.25 13.957L13.957 13.25L13.6055 12.8945L8.70703 8L13.957 2.75L13.25 2.04297L8 7.29297L3.10156 2.39844L2.75 2.04297Z" id="Shape" fill="#111111" stroke="none" />
            </g>
            </g>
          </svg>
        </button>
        <div class="formulaire">
          <form action="">
            <label for="mail">
              Email:
              <input type="email" name="" id="mail" placeholder="mouzx@y.com">
            </label>
            <label for="password">
              Mot de passe:
              <input type="password" name="" id="password" placeholder="mot de passe">
            </label>
            <div class="submit">
              <button type="submit"> Connexion</button>
            </div>
          </form>
        </div>
        <div class="description">
          <p>Vous n'avez pas de compte? <span @click="openLinkConnexion">Cliquez-vous ici</span></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'logUser',
  data () {
    return {
      showModalSignUp: false,
      showModalSignIn: false,
      isActive: true
    }
  },
  methods:{
    openLinks(){
      if(this.showModalSignUp = true){
        this.showModalSignUp = false,
        this.showModalSignIn = true        
        console.log('Inscription ');
      } 
    },
    openLinkConnexion(){
      if(this.showModalSignIn = true){
        this.showModalSignIn = false,
        this.showModalSignUp = true        
        console.log('Connexion ');
      } 
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .isActive{
    position: fixed;  
    width: 350px;
    background: rgb(255, 255, 255);
    border-radius: 15px;
    padding: 20px;
    z-index: 9999;
    box-shadow: 0 0 10px #212121e0, 100px 100px 100px 9000em rgb(48 47 47 / 74%);
    opacity: 0;
    animation-name: appear;
    animation-duration: .5s;
    animation-timing-function: cubic-bezier(0.45, 0.04, 0.69, 1.15);
    animation-delay: .1s;
    animation-duration: alternate;
    animation-fill-mode: forwards;
    transition: ease-out 3s;
  }

  @keyframes appear {
    0%{
      transform: translate(150%, -90%);
      /* opacity: .5;  */
      /* transform: scale(0); */
    }
    100%{
      opacity: 1;
      /* transform: scale(1); */
      transform: translate(150%, 10%);
    }
  }

  .log .formulaire{
    width: 100%;
  }
  .log .formulaire label{
    display: flex;
    flex-direction: column;
    font-size: 22px;
    margin: 15px 0;
  }
  .log .formulaire label input{
    width: 100%;
    padding: 10px 5px;
    font-size: 16px;
    border-radius: 5px;
    outline: none;
    background: #e6e6e6;
    border: none;
  }
  button{
    outline: none;
    border: none;
    padding: 5px;
    border-radius: 5px;
    cursor: pointer;
  }
  .log button.close-icon{
    position: absolute;
    top: 10px;
    right: 10px;
    background: none;
  }
  .log button.close-icon svg{
    height: 32;
    width: 32px;
  }
  .formulaire button{
    background: #663399;
    color: #fff;
    width: 100%;
    margin: 0 0 15px 0;
    padding: 10px 5px;
    font-size: 16px;
  }
  .description span{
    font-size: 13px;
    font-weight: 700;
    color: #663399;
    cursor: pointer;
  }

</style>
