<template>
	<MainMenu/>
	<div class="wrapper">
		<div class="calendar-carousel pb-4 d-flex" id="calendar-carousel"></div>

		<div class="row">
			<div class="col-8">
				<div class="block daily-playlist" id="daily-playlist">
					<div class="daily-playlist-header p-2" id="daily-playlist-header"></div>
					<div v-for="(name, artist, idx) of currentPlaylist" v-bind:key="idx">
						<SongRow v-bind:artist="artist" v-bind:name="name"/>
					</div>
				</div>
			</div>
			<div class="col-4">
				<div class="block about-daily-playlist my-3">
					<div class="block uniqueness-percent p-3">
						<p>на сколько уникален</p> 
						<p>подробней</p>
					</div>
					<div class="more-details">
						<p>3 песни совпадают с моими аудио</p>
						<p>17 песен встречались ранее</p>
						<p>если кликнуть щирина колонки станет 8 и появится график</p>
					</div>
				</div>
			</div>
		</div>


		<p>инфографика</p>
		<p>сначала за сегодняшний день, сколько песен из дневного плейлиста есть в моей музыке, сколько песен из него же есть в предыдущих плейлистах</p>
		<p>где-то нужно вывести график как с течением времени уменьшается количество уникальных песен в ежедневниках</p>

	</div>
	<AboutNote/>
</template>


<script>
import MainMenu from './MainMenu.vue'
import AboutNote from './AboutNote.vue'
import SongRow from './SongRow.vue'

export default {
	name: 'MainPage',
	components: {
		MainMenu,
		AboutNote,
		SongRow,
	},
	data() {
		return {
			monthList: ['Январь', 'Февраль', 'Март', 'Апрель', 'Май', 'Июнь', 'Июль', 'Август', 'Сентябрь', 'Октябрь', 'Ноябрь', 'Декабрь'],
			getLastDailyPlaylist: 'http://localhost:1111/lastGetedPlaylist',
			currentPlaylist: {}
		}
	},
	async mounted() {
		const response = await fetch(this.getLastDailyPlaylist, {
			method: 'POST',
			headers: { 
				'Content-Type': 'application/json;charset=utf-8' 
			}
		})
		

		if (response.ok) {
			let data = (await response.json()).data
			let playlistDate = new Date(data['date'])

			this.setCurrentMonth(playlistDate.getMonth())

			let a = document.createElement('a')
			a.classList.add('calendar-day')
			a.innerText = playlistDate.getDate()
			document.getElementById('calendar-carousel').append(a)
			
			this.currentPlaylist = data.playlist

			this.setDateActivePlaylist(playlistDate.getDate(), playlistDate.getMonth()+1, playlistDate.getFullYear())
		} else {
			alert("Ошибка HTTP: " + response.status)
		}
	},
	methods: {
		displayCalendar() {

		},
		setCurrentMonth(month) {
			document.getElementById('current-month').innerText = this.monthList[month]
		},
		setDateActivePlaylist(day, month, year) {
			document.getElementById('daily-playlist-header').innerText = `Плейлист от ${day}.${month}.${year}`
		},
		addSong(artist, name) {
			let songBlock = document.createElement('div')

			songBlock.style.padding = '8px'
			songBlock.style.margin = '8px'
			songBlock.style.borderRadius = '5px'
			songBlock.style.background = '#edeef0'
			songBlock.style.textAlign = 'left'
			songBlock.innerText = artist
			songBlock.innerText += ' - ' + name

			return songBlock
		}
	}
}
</script>


<style>
a {
	text-decoration: none !important;
	color: black !important;
	cursor: pointer;
	transition: .1s;
}
a:hover {
	color: #0077ff;
}
.wrapper {
	max-width: 1200px;
	padding: 0 30px;
	margin: auto;
}
.current-month-wrapper {
	margin-left: -20px;
}
.current-month-wrapper > i {
	color: transparent;
	transition: .1s;
}
.current-month-wrapper:hover > i {
	color: black;
}
.calendar-carousel {
	overflow: hidden;
}
.calendar-day {
	width: 40px;
	height: 40px;
	margin-right: 6px;
	border-radius: 6px;
	background: black;
	line-height: 40px;
	font-size: 20px;
	color: white !important;
	cursor: pointer;
	transition: .1s;
}
.calendar-day:hover {
	background: #0077ff;
}
.block {
	position: relative;
	width: 100%; 
	border-radius: 12px;
	background: white;
}
.daily-playlist {
	overflow: hidden;
	overflow-y: auto;
	height: 400px;
}
.daily-playlist::-webkit-scrollbar {
	width: 0px;
}
.daily-playlist-header {
	margin-left: auto;
	margin-right: 0;
	border-radius: 12px;
	background-color: #0077ff;
	color: white;
}
.about-daily-playlist {
	height: 400px;
	cursor: pointer;
}
.about-daily-playlist:hover {
	box-shadow: 0 0 10px 10px #00000005;
}
.uniqueness-percent {
	background: #0077ff;
	color: white;
}
</style>
