<template>
    <div class="user">
      <topMenuUser :userInfos="userInfos" :firstLetter="firstLetter" :secondLetter="secondLetter" ref="topMenuUser"/>
      <bannerCover ref="bannerCover" />
      <div class="items-section">
        <div class="user-infos">
          <userInfos :userInfos="userInfos" :firstLetter="firstLetter" :secondLetter="secondLetter" ref="UserInfomation"/>
        </div>
        <div class="user-tab">
          <div class="btn-content">
            <button v-for="(tab, index) in tabs" :key="index" @click.prevent="setCurrentComponent(tab.component, index)" class="btn-tabs" :class="{'active' : isActive === index}">
              {{tab.name}}
            </button>
          </div>       
          <keep-alive>
            <component :is="currentComponent" />
          </keep-alive>
        </div>
      </div>
      <router-view/>
    </div>
  </template>
  
  <script>
    import aboutUser from './aboutUser';
    import myArticles from './myArticles';
    import topMenuUser from './topMenuUser';
    import bannerCover from './bannerCover';
    import userInfos from './userInfos';
    import { auth, db } from '../../../firebase';
    import { collection, doc, getDocs } from "firebase/firestore"; 
    import { onAuthStateChanged } from 'firebase/auth';
    export default {
      name: 'userProfile',
      components:{
        aboutUser,
        myArticles,
        topMenuUser,
        bannerCover,
        userInfos
      },
      data (){
        return{
          avatarUser:'https://avatoon.me/wp-content/uploads/2020/07/Cartoon-Pic-Ideas-for-DP-Profile-03.png', 
          userInfos:{},
          firstLetter: '',
          secondLetter: '',
          tabs:[{name:'A Propos de moi', component:'aboutUser'},
          {name:'Mes Articles', component:'myArticles'}],
          currentComponent: "aboutUser",
          isActive: 0,
        }
      },
      methods:{
        setCurrentComponent(component, index) {
          this.currentComponent = component
          this.isActive = index
        },
        getUserData(){
          onAuthStateChanged(auth,(user) =>{
            if(user != null){
              let getName = user.displayName
            }
          })
        },
        async getUser(){
          this.getUserData()
          let querySnapshot = await getDocs(collection(db, "users"))
          querySnapshot.forEach((doc) => {
            this.userInfos = {
              infoUser: {
                name: doc.data().name,
                lastName: doc.data().lastName, 
              },
              uid: doc.data().uid
            },
            localStorage.setItem('userSession', JSON.stringify(this.userInfos))
            this.firstLetter = this.userInfos.infoUser.name.charAt(0)
            this.secondLetter = this.userInfos.infoUser.lastName.charAt(0)
            // this.firstLetter = this.userInfos.infoUser.charAt(0)
            console.log('infos users :', this.userInfos.infoUser.name.charAt(0));
          })
        }      
      },
      mounted(){
        this.getUser()
      }
    }
  </script>
  
  <style scoped>
  
    /* partie du conténu user-infos */
    .items-section{
      display: flex;
      align-items: start;
      margin: 2% 10%;
    }
    .items-section .user-infos {
      flex: 1;
    }
    .items-section .user-tab{
      flex: 2;
    }
   
    .items-section button.link-btn a h1{
      margin-bottom: 10px;
      font-size: 1.5rem;
    }
  
    .btn-content{
      display: flex;
      justify-content: first baseline;
      margin-bottom: 10%;
      position: relative;
      padding-bottom: 8px;
      border-bottom: 2px solid var(--border-gray-thin);
      z-index: 1;
    }
    .btn-content button{
      padding: 8px 15px;
      font-size: 1.1rem;
      outline: none;
      border: none;
      cursor: pointer;
      background: transparent;
    }
    .btn-content button:hover{
      color: var(--hover-link-gray);
      transition: all ease-in-out .3s;
    }
    .btn-content button.active{
      position: relative;
      color: var( --active-color-purple);
    }
    .btn-content button.active::before{
      content: '';
      position: absolute;
      bottom: 0;
      height: 2px;
      width: 100%;
      transform: translate(-15px, 10px);
      background: var(--background-btn-purple-light);
    }
  </style>