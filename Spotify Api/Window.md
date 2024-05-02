#SpotifyAPI #Spotify #API #JavaScript 

```Javascript
window.onSpotifyWebPlaybackSDKReady = () => {
  const token = '[My access token]';
  const player = new Spotify.Player({
    name: 'Web Playback SDK Quick Start Player',
    getOAuthToken: cb => { cb(token); },
    volume: 0.5
  });
```

- Method
- Creates an instance of player with these parameters:
	- name of spotify instance
	- callback getOAuthToken (provides a valid access_token)
	- volume of player (0 < volume < 1)
