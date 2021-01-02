<template>
  <body>
    <div class="about">
      <HelloWorld msg="Spotify API for learning Vue.js" />

      <Dropdown
        label="Genre: "
        :genreList="listOfGenres"
        :genreChange="onGenreChange"
        v-on:valueChanged="getPlaylist"
      />
      <Dropdown
        label="Playlist: "
        :genreList="listOfPlaylist"
        v-on:valueChanged="getSongs"
      />

      <ListBox :listOfSongs="listOfTracks" v-on:buttonClicked="setDetail" />
      <Detail v-if="safeToLoad" :trackDetails="trackDetail" />
    </div>
  </body>
</template>
<script>
import axios from "axios";
import Dropdown from "./components/Dropdown.vue";
import HelloWorld from "./components/HelloWorld.vue";
import ListBox from "./components/ListBox.vue";
import Detail from "./components/Detail.vue";

export default {
  name: "App",
  components: {
    Dropdown,
    HelloWorld,
    ListBox,
    Detail,
  },

  data() {
    let client_id = " *** "; // Your client id
    let client_secret = " *** "; // Your secret

    return {
      client_secret,
      client_id,
      key: "",
      listOfGenres: [],
      listOfPlaylist: [],
      listOfTracks: [],
      trackDetail: [],
      safeToLoad: false,
    };
  },
  methods: {
    getPlaylist(data) {
      axios(
        `https://api.spotify.com/v1/browse/categories/${data}/playlists?limit=10`,
        {
          method: "GET",
          headers: { Authorization: "Bearer " + this.key },
        }
      ).then((playlistResponse) => {
        this.listOfPlaylist = playlistResponse.data.playlists.items;

        console.log(this.listOfPlaylist);
      });
    },
    getSongs(data) {
      console.log("This is the song data");
      console.log(data);

      axios(`https://api.spotify.com/v1/playlists/${data}/tracks?limit=10`, {
        method: "GET",
        headers: { Authorization: "Bearer " + this.key },
      }).then((tracksResponse) => {
        this.listOfTracks = tracksResponse.data.items;
        console.log(this.listOfTracks);
      });
    },
    setDetail(data) {
      console.log("this is the data from main song id " + data);

      const currentTracks = [...this.listOfTracks];

      const trackInfo = currentTracks.filter((t) => t.track.id === data);

      this.trackDetail = trackInfo[0].track;
      this.safeToLoad = true;
      console.log(this.trackDetail);
    },
  },
  async mounted() {
    await axios("https://accounts.spotify.com/api/token", {
      headers: {
        "Content-Type": "application/x-www-form-urlencoded",
        Authorization:
          "Basic " + btoa(this.client_id + ":" + this.client_secret),
      },
      data: "grant_type=client_credentials",
      method: "post",
    }).then((tokenResponse) => {
      this.key = tokenResponse.data.access_token;

      axios
        .get("https://api.spotify.com/v1/browse/categories?locale=sv_US", {
          method: "GET",
          headers: { Authorization: "Bearer " + this.key },
        })
        .then((genreResponse) => {
          this.listOfGenres = genreResponse.data.categories.items;
          console.log(genreResponse.data.categories.items);
        });
    });
  },
};
</script>

<style scoped>
div {
}
.about {
  text-align: center;
}
</style>