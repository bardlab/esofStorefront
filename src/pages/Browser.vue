<template>
<div id='app'>
  <ShowDetails v-if="showInfo===true" @close="showInfo=false" v-bind:session="infoStore"/>
    <Header/>
  <div class="container  mb-3 p-10 max-w-5xl flex flex-row font-light">
      <div class="self-center w-1/3 mx-3">
            <img src="../assets/themes_transparent.png" alt="Conference Themes"/>
      </div>

      <div class="self-center w-2/3 mx-3 text-justify text-lg">
        <p>
          On this page you are able to browse a mock-up conference program, which serves as an example of the work done internally in the realm of CMS development. 
          To avoid trademark and/or privacy-related issues (the official program is available at <a href="https://www.esof.eu/en/programmes/science-programme.html">esof.eu</a> )
          all names, affiliations and titles have been anonymized with a custom program developed in-house.<br/>
          Click on the themes below to explore the conference program. By clicking on the <span class="text-gray-500 text-xl font-bold">+</span> icon, you can add proposals of interest to your personal selection, which will be displayed at the bottom of the page.
        </p>
      </div>
  </div>

    <div class="container border-t border-b border-gray-400 mb-20 py-5 max-w-5xl flex flex-row flex-wrap justify-center" >
      <div v-for='theme in allThemes' v-bind:key='theme.Short'><RndButton v-bind:theme="theme" v-on:changeActiveTheme="changeTheme"/></div>
    </div>

    <div class="container border-b border-gray-400 mb-10 p-3 max-w-5xl">
      <p class="text-center font-light text-sm m-0">Currently browsing theme... </p>
      <h1 class="text-center text-3xl font-sans pb-3 font-light">{{displayedTheme}}</h1>
    </div>

    <div class="container flex flex-row flex-wrap items-stretch mx-auto mt-10 mb-3 p-0 max-w-5xl font-sans text-lg">
      <div class="w-1/3 p-2 font-light self-start my-2" v-for='session in displayedSessions' v-bind:key='session.Reference' >
        <div class="">
          <p>July {{session.Day}}th at {{session.Time}}</p>
          <p class="font-normal">{{session.Title}}</p>
          <p>from the {{session.Affiliation}}</p>
        </div>
        <div class="flex flex-row items-center content-center justify-start my-2">
          <div class="button flex flex-row content-center" v-if="session.isSelected === 0" @click="toggle_isSelected(session)">
              <button class="self-center mx-auto "> <img class="h-8 w-8 opacity-25 hover:opacity-75" src="../assets/plus.png" alt=""></button>
              <p class="ml-3 mr-5 self-center">Select</p>
          </div>
          <div class="button flex flex-row content-center" v-if="session.isSelected === 1" @click="toggle_isSelected(session)">
              <button  class="self-center mx-auto" ><img class="h-8 w-8  opacity-25 hover:opacity-75" src="../assets/minus.png" alt=""> </button>
              <p class="ml-3 mr-5 self-center">Remove</p>
          </div>
          <div class="button flex flex-row content-center" @click="showDetails(session)">
              <button  class="self-center mx-auto content-center" ><img class="h-8 w-8  opacity-50 hover:opacity-100" src="../assets/information.png" alt=""> </button>
              <p class="ml-3 self-center">Details</p>
          </div>
        </div>
      </div>
    </div>


    <div class="container border-b border-gray-400 mb-10 p-3 max-w-5xl">
      <h1 class="text-center text-3xl font-sans p-3 font-light">Selection</h1>
    </div>

    <div class="container flex flex-col mx-auto my-10 font-sans text-lg mb-10 max-w-5xl">
        <ul class="flex border-b border-gray-400">
          <li class="-mb-px mr-1">
            <button class="bg-white inline-block py-2 px-4 text-gray-800 font-light hover:font-semibold" v-bind:class="isTableActive(6)" @click="selectedDay = 6">Day 1</button>
          </li>
          <li class="mr-1">
            <button class="bg-white inline-block py-2 px-4 text-gray-800 font-light hover:font-semibold" v-bind:class="isTableActive(7)" @click="selectedDay = 7">Day 2</button>
          </li>
          <li class="mr-1">
            <button class="bg-white inline-block py-2 px-4 text-gray-800 font-light hover:font-semibold" v-bind:class="isTableActive(8)" @click="selectedDay = 8">Day 3</button>
          </li>
          <li class="mr-1">
            <button class="bg-white inline-block py-2 px-4 text-gray-800 font-light hover:font-semibold" v-bind:class="isTableActive(9)" @click="selectedDay = 9">Day 4</button>
          </li>
        </ul>

        <table class="table-auto border-collapse mt-5 w-full" >
          <thead class="text-left" v-if="selectedSessions.sort(sortSessions).filter(session => session.Day === selectedDay).length > 0">
            <tr>
              <th class="font-sans font-normal text-left px-2 py-1 w-3/7">Title</th>
              <th class="font-sans font-normal text-left px-2 py-1 w-3/7">Organizer</th>
              <th class="font-sans font-normal text-left px-2 py-1 w-1/7">Time</th>
            </tr>
          </thead>
          <tbody class="text-left mt-5">
            <tr v-for="session in selectedSessions.filter(session => session.Day === selectedDay)" v-bind:key="session.Reference">
              <th class="font-sans font-light text-left px-2 py-1">{{session.Title}}</th>
              <th class="font-sans font-light text-left px-3 py-1">{{session.Affiliation}}</th>
              <th class="font-sans font-light text-left px-2 py-1">{{session.Time}}</th>
            </tr>
          </tbody>
        </table>
    </div>

</div>
</template>

<script>
import Header from '../components/Header';
import Sessions from "../data/anonProgrammeDump.json";
import Science from "../data/themes_science.json";
import S2B from "../data/themes_s2b.json";
import Careers from "../data/themes_careers.json";
import ShowDetails from "../components/ShowDetails";
import RndButton from "../components/rndButton";

export default {
  name:"Browser",
  metaInfo: {
    title: 'Program Browser',
    meta: [
      {name: "LB"}
    ]
  },
	components: {
    Header,
    ShowDetails,
    RndButton
	},
  data(){
	  return {
      Sessions,
      Science, 
      S2B, 
      Careers,
      displayedTheme: '',
      selectedDay: 0,
      showInfo: false, 
      infoStore: {}
      }
  }, 
  methods: {
    changeTheme(newTheme){
      this.displayedTheme = newTheme;
    },
    toggle_isSelected(s){
      s.isSelected = s.isSelected == 1 ? 0 : 1;
    },
    showDetails(s){
      this.infoStore = s;
      this.showInfo = true;
    },
    isTableActive(cur){
      return {
        "border-b-2 border-blue-300 font-bold": this.selectedDay == cur
        }
    },
    sortSessions(a, b){
      return a.Time > b.Time;
    }
  },
  computed: {
    displayedSessions(){
      return this.Sessions.filter(session => session.Theme === this.displayedTheme);
    },
    selectedSessions(){
      return this.Sessions.filter(session => session.isSelected === 1 );
    },
    allThemes(){
      return Careers.concat(S2B).concat(Science); 
    }
  },
  created() {
    this.displayedTheme = "Value-Driven Innovation";
    this.selectedDay = 6;
  }
}
</script>
