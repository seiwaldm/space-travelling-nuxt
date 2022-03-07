<template>
  <div>
    <h1 class="numbered-title"><span>01</span> Pick your destination</h1>
    <div id="content" v-if="destination">
      <img :src="destination['png-image'].guid" alt="Mond-Foto" />
      <ul>
        <li
          v-for="(item, index) in destinations"
          :key="item['destination-name']"
          @click="setDestination(index)"
        >
          {{ item['destination-name'] }}
        </li>
      </ul>
      <h1>{{ destination['destination-name'] }}</h1>
      <p>{{ destination.description }}</p>
      <div>
        <span>{{ destination.distance }}</span>
        <span>{{ destination.travel }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      destinations: [],
      activeDestinationIndex: 3,
    }
  },
  computed: {
    destination() {
      return this.destinations[this.activeDestinationIndex]
    },
  },
  methods: {
    async loadData() {
      const response = await fetch(
        'https://space.wp.seiwald.hak-stjo.schulwebspace.at/wp-json/wp/v2/destination'
      )
      this.destinations = await response.json()
    },
    setDestination(index) {
      this.activeDestinationIndex = index
    },
  },
  mounted() {
    this.loadData()
    document.body.style.backgroundImage =
      "url('background-destination-mobile.jpg')"
  },
}
</script>

<style scoped>
.numbered-title {
  font-size: 16px;
}
</style>
