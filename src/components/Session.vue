<template>
<div>
        <div class="tile is-child is-light">
          <p>July {{session.Day}}th at {{session.Time}}</p>
          <p class="subtitle">{{session.Title}}</p>
          <p>from the {{session.Affiliation}}</p>
        </div>
        <div class="tile is-child">
          <div class="buttons" v-if="session.isSelected === 0" @click="toggle_isSelected(session)">
              <b-button type="is-light" expanded>Add to Selection</b-button>
          </div>
          <div class="buttons" v-if="session.isSelected === 1" @click="toggle_isSelected(session)">
              <b-button type="is-light" expanded>Remove from Selection</b-button>
          </div>
              <ShowDetails v-bind:session="session" />
        </div>
</div>

</template>

<script>
export default {
    name: 'Session',
    props: ['session']
}
</script>