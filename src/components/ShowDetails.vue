<template>
<div class="fixed pin -mt-10 z-50 overflow-auto bg-white opacity-75 h-screen w-screen flex" @click="$emit('close')">
  <div class="relative p-10 w-full max-w-lg m-auto flex-col flex border-t-2 border-blue-400 rounded-b self-center opacity-100">
    <div class="">
      <p class="font-bold text-xl">{{session.Title}}</p>
      <p class="text-sm">{{session.Affiliation}}</p>
      <p class="mt-3 mb-1 font-bold">Speakers</p>
      <p class="py-1" v-bind:key="speaker[0]" v-for="speaker in session.Speakers">{{speaker[0]}} ({{speaker[1]}})</p>
      <p class="mt-3 mb-1 font-bold">Abstract</p>
      <p class="my-3">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nesciunt reiciendis architecto eos ea. Odio error exercitationem pariatur cum sunt ratione itaque repellat voluptatem. Ipsa enim unde, similique quisquam animi quia praesentium nemo! Natus laboriosam voluptatibus dignissimos molestias! Nam error, vitae blanditiis harum, porro accusantium tenetur repellat aliquam pariatur iste molestias?</p>
    </div>
  </div>
</div>
</template>

<script>
export default {
    name: 'Session',
    props: ['session']
}
</script>