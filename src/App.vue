<template>
  <div id="app">
    <h3>List of Episodes</h3>
    <!-- {{ "p" + pending }} -->
    <div style="display: flex; border: 1px solid red">
      <div
        class="shows"
        v-for="episode in episodes.slice(0, 3)"
        :key="episode.id"
      >
        <div style="display: flex; flex-direction: column; height: 200px">
          <span>{{ episode.name + " SERVER" }}</span>
          <img :src="episode.image.medium" />
        </div>
      </div>

      <div
        class="shows"
        v-for="episode in episodes.slice(3, 6)"
        :key="episode.id"
        style="display: flex; border: 1px solid blue"
      >
        <div style="display: flex; flex-direction: column; height: 200px">
          <span>{{ episode.name + "from client" }}</span>
          <img :src="episode.image.medium" />
        </div>
      </div>
    </div>

    <video
      v-for="n in 20"
      :key="n"
      width="320"
      height="240"
      autoplay
      loop
      preload="metadata"
      muted
    >
      <source src="@/assets/sample-mp4-file.mp4" type="video/mp4" />
      Your browser does not support the video tag.
    </video>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    episodes: [],
  }),
  async created() {
    const d = await fetch("https://api.tvmaze.com/shows/662?embed=episodes");
    const x = await d.json();
    this.episodes = x._embedded.episodes;
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
