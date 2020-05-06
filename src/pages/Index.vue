<template>
<div class="flex flex-col  font-light text-lg text-justify">
<Header/>

<div class="container mb-10 p-10 max-w-5xl">
  <p>
		ESOF2020 is the latest in a series of 5-day international conferences sponsored by Euroscience. These conferences bring together policy makers, 
		scientists and entrepreneurs to discuss future developments at the interface between science and policy.<br/>
		The conference format comprises three tracks (Science, Careers and Science to Business) with 18 themes, each of which was drafted from scratch in collaboration with 
		international collaborators. This website is a short summary of the work performed as an analytst and program officer for the conference by me, Luca Bardini.  
  </p>
<div class="container relative flex flex-row object-center mx-auto mt-20 font-sans text-lg mb-10 max-w-4xl">
  <div class="mx-auto  text-center">
      <p class="font-normal text-2xl">18</p>
      <p class="">Themes</p>
  </div>
  <div class="mx-auto  text-center">
      <p class="font-normal text-2xl">{{Object.values(countryStats).reduce((a,b) => a+b )}}+</p>
      <p class="heading">Sessions</p>
  </div>
  <div class="mx-auto  text-center">
      <p class="font-normal text-2xl">{{Object.keys(countryStats).length}}+</p>
      <p class="heading">Countries</p>
  </div>
  <div class="mx-auto  text-center">
      <p class="font-normal text-2xl">900+</p>
      <p class="heading">Speakers</p>
  </div>
</div>
<!--	<div class="max-w-4xl mx-auto my-5">
    <img src="../assets/world.png" alt="Geographical distribution">
  </div>-->
	<div class="max-w-4xl mx-auto my-5">
    <GChart
    type="GeoChart"
    :data="gChartData"
    :options="{
        colorAxis: {'colors': ['#00853f', '#00853f']},
        magnifyingGlass : {enable: true, zoomFactor: 7.5},
        legend: 'none',
        chart: {
          title: 'Global Participation',
          subtitle: 'Number of sessions from participating countries',
        }
      }"
  />
  </div>
</div>

<div class="container mb-10 p-10 max-w-5xl" id="analytics">
  <h2 class="text-3xl font-thin text-center mb-10 border-b border-gray-400">Conference Analytics</h2>
  <div class="container flex flex-row ">
    <p class="my-5 self-start w-1/2 px-3">
        The call for proposals resulted in <b>600 submissions</b>, spread among the 18 conference themes, for a total of roughly <b>4000 speakers</b>. 
        Of the received submissions, less than 25% made it into the final programme.<br/>
        To properly <b>manage, screen and monitor</b> the proposal refereeing and selection processes a variety of custom analytics and data visualization schemes were 
        developed. 
    </p>
    <p class="my-5 self-start w-1/2 px-2">
        All the graphics on this website are examples of the work performed. <br/>
        Particular attention was devoted to covering current <b>hot-topics</b> and <b>keywords</b> through a semi-automated textual analysis of proposals, as well as to ensure balance in gender and geographical provenance. <br/>
    </p>
</div>
	<div class="max-w-3xl mx-auto mb-5">
    <img src="../assets/sankey.png" alt="Themes and keywords distribution">
  </div>

	<p class="my-5">
      In order to achieve this result, my reponsabilities involved a range of activities from the creation of the content for the conference themes and call for 
      proposals, the coordination of the reviewing and grading process through the creation of custom conference analytics, to the management of public relations 
      with international collaborators and attendees. 
      A high level of automation, through the development of custom software, was instrumental in making the workload not just manageable, 
      but efficient and less prone to human error. An overview of the tools I employed can be found in the <a class="text-blue-300 font-bold hover:text-blue-500" href="/about">About</a> section.
  </p> 
</div>

<div class="container mb-10 p-10 max-w-5xl" id="print">
  <div class="text-3xl font-thin items-center text-center mb-10 border-b border-gray-400">Printed materials</div>
	<p class="mx-auto my-5">
    A number of printed materials were created in order to report results as well as to promote/illustrate the conference programme to internal and external stakeholders. 
    In order to include the latest available data in real-time, part of the creation of internal reports was also automated with custom scripts.
	</p>

	<div class="flex flex-row object-center my-5">
		<div class="">
      <img src="../assets/numbers.png" alt="Graphic design example 1">
    </div>	
		<div class="">
      <img src="../assets/pamphlet.png" alt="Graphic design example 2">
    </div>
		<div class="">
      <img src="../assets/propList.png" alt="Graphic design example 3">
    </div>
	</div>
</div>

</div>
</template>

<script>
import Header from '../components/Header';
import { GChart } from 'vue-google-charts';
import programme from '../data/anonProgrammeDump.json';

export default {
  name: "Home",
	metaInfo: {
		title: 'ESOF Storefront',
    meta: [
      {name: "LB"}
    ]
  },
	components: {
    Header,
    GChart,
  },
  data(){
    return{
      programme, 
      countryStats: new Object()
    }
  },
  computed: {
    gChartData(){
      var gChartData = Object.keys(this.countryStats).map( (k) => [k, this.countryStats[k]] );
      gChartData.unshift( ['Country', 'Sessions'] );
      return gChartData;
    }
  },
  created() {
    this.programme.map( (e) => {
      if (this.countryStats.hasOwnProperty(e.Country) )
      {
          this.countryStats[e.Country] += 1; 
      } else {
          this.countryStats[e.Country] = 1; 
      }
    });
  }

}
</script>

<style>


</style>