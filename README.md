# spotify_playlist_api

This is a simple project dedicated to learning Vue.js. You can select a genre of music. After that you can select a playlist witch displays the songs on that playlist. After clicking on a song the album cover is displayed.

## Project setup
```
npm install
```

### How to run the project
```
npm run serve
```

### Usage

You need a spotify acc: https://developer.spotify.com/

You can enter the needed id and secret in the App.vue file

```javascript
data() {
let client_id = " ENTER THE SPOTIFY CLIENT ID"; // Your client id
let client_secret = "ENTER THE SECRET"; // Your secret
...
```

#### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
