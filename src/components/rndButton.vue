<template>
    <div class="p-2 self-center font-light" v-bind:class="randomFont()" v-on:click="$emit('changeActiveTheme', theme.Long)">
        <button >{{theme.Short}}</button>
    </div>
</template>

<script>
export default {
    name: 'RndButton',
    props: ['theme'],
    data(){
        return{
            rndColors: ['pink-700', 'purple-700', 'indigo-700', 'blue-400', 'green-700', 'yellow-800', 'orange-700', 'teal-800', 'red-600', 'gray-700'],
            rndSizes: ['text-3xl', 'text-xl', 'text-2xl']
        }
    },
    methods:{
        randomFont(){
        return 'text-'+this.rndColors[Math.floor(Math.random() * (this.rndColors.length + 1))] + ' ' + this.rndSizes[Math.floor(Math.random() * (this.rndSizes.length + 1))];
        }
    }
}
</script>