<template>
<div class="flex flex-col font-light text-lg text-justify">
  <Header/>

  <div class="container mb-10 p-10 max-w-4xl">
    <p>
      The core of the work, in terms of <b>Analytics, Data Visualization and development</b> was performed in Python, Matplotlib and Pandas. <br/>
      In order to <b>share information</b> with collaborators, routines were developed to export the needed data in the desired formats (docx, xlsx, pdf). Excel was also 
      used extensively to develop reports and other project management tools through the use of pivot tables.<br/>
    </p>
    <div class="max-w-3xl mx-auto my-5">
      <img src="../assets/tools.png" alt="Tools">
    </div>
    <p>
      The data were monitored, analyzed, interpreted and used to enable <b>evidence-based decision making</b> on a daily basis, both with regard to my personal work, as well 
      as to support the work of colleagues.<br/>
      Last but not least, this website is the result of a full-stack project in Vue.js, a Javascript framework.
    </p>
	</div>

</div>
</template>

<script>
import Header from '../components/Header';

export default {
  name:"About",
  metaInfo: {
    title: 'About',
    meta: [
      {name: "LB"}
    ]
  },
	components: {
		Header
	}
}
</script>
