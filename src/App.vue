<template>
	<div id="app">
		<header>
			<h1>My Music</h1>
		</header>
		<main>
			<section class="player">
				<h2 class="song-title">{{ current.title }} ~ <span>{{ current.artist }}</span></h2>
				<div class="controls">
					<button class="prev" @click="prev">Pre</button>
					<button class="play" v-if="!isplay" @click="play">Play</button>
					<button class="pause" v-if="isplay" @click="pause">Pause</button>
					<button class="next" @click="next">Next</button>
				</div>
			</section>
			<div class="playlist">
				<h3>This Playlist</h3>
				<div class="songs">
					<button 
						v-for="song in songs" 
						:key="song.src" 
						@click="play(song)" 
						:class="(song.src == current.src ? 'song playing' : 'song')">
						{{ song.title }} ~ {{ song.artist }}
					</button>
				</div>
			</div>
		</main>
	</div>
</template>

<script>
export default {
	name: 'app',
	data() {
		return {
			current: {},
			index: 0,
			isplay: false,
			songs: [
				{
					title: 'Romantic',
					artist: 'Unknown',
					src: require('./assets/1.mp3')
				},
				{
					title: 'Romantic',
					artist: 'Unknown',
					src: require('./assets/2.mp3')
				},
				{
					title: 'Sad',
					artist: 'Unknown',
					src: require('./assets/3.mp3')
				}
			],
			player: new Audio(),
		}
	},
	methods: {
		play(song) {
			if(typeof song.src != "undefined") {
				this.current = song;

				this.player.src = this.current.src;
			}
			this.player.play();
			this.isplay = true;
		},
		pause () {
			this.player.pause();
			this.isplay = false;
		},
		prev () {
			this.index--;
			if(this.index < 0) {
				this.index = this.songs.length - 1;
			}

			this.current = this.songs[this.index];
			this.play(this.current);
		},
		next () {
			this.index++;
			if(this.index > this.songs.length -1) {
				this.index = 0;
			}

			this.current = this.songs[this.index];
			this.play(this.current);
		},
	},
	created () {
		this.current = this.songs[this.index];
		this.player.src = this.current.src;
		// this.player.play();
	}
}
</script>
<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
body {
	font-family: 'Poppins', sans-serif;
	background-color: #1f1f1f;
	color: #EEE;
}

header {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 20px;
	background-color: #333;
	color: #FFF;
	box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
}

h1 {
	font-size: 32px;
	font-weight: 600;
	text-transform: uppercase;
	letter-spacing: 3px;
}

main {
	width: 100%;
	max-width: 900px;
	margin: 20px auto;
	padding: 25px;
	background-color: #282828;
	border-radius: 10px;
	box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3);
}

.song-title {
	font-size: 28px;
	font-weight: 700;
	text-transform: uppercase;
	color: #EEE;
	text-align: center;
	margin-bottom: 20px;
}

.song-title span {
	font-weight: 400;
	font-style: italic;
}

.controls {
	display: flex;
	justify-content: center;
	align-items: center;
}

button {
	background: none;
	border: none;
	cursor: pointer;
	transition: transform 0.3s, opacity 0.3s;
}

button:hover {
	opacity: 0.8;
	transform: scale(1.1);
}

.play, .pause {
	font-size: 22px;
	font-weight: 700;
	padding: 15px 25px;
	border-radius: 30px;
	color: #FFF;
	background-color: #F64C72;
	box-shadow: 0 6px 12px rgba(246, 76, 114, 0.3);
}

.play:hover, .pause:hover {
	background-color: #FF4757;
}

.next, .prev {
	font-size: 16px;
	font-weight: 700;
	padding: 10px 20px;
	border-radius: 20px;
	color: #FFF;
	background-color: #444;
	box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
}

.next:hover, .prev:hover {
	background-color: #F64C72;
}

.playlist {
	margin-top: 30px;
}

.playlist h3 {
	font-size: 24px;
	font-weight: 400;
	color: #EAEAEA;
	text-align: center;
	margin-bottom: 20px;
}

.songs {
	display: flex;
	flex-direction: column;
	gap: 10px;
}

.song {
	display: flex;
	justify-content: space-between;
	padding: 12px 20px;
	font-size: 18px;
	font-weight: 600;
	color: #EEE;
	background-color: #333;
	border-radius: 6px;
	cursor: pointer;
	transition: all 0.3s ease;
}

.song:hover {
	background-color: #444;
	color: #F64C72;
}

.song.playing {
	color: #FFF;
	background: linear-gradient(135deg, #F64C72, #FF4757);
	box-shadow: 0 4px 10px rgba(246, 76, 114, 0.3);
}
</style>