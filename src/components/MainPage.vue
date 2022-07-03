<template>
	<div class="wrapper">
		<div class="calendar">
			<div class="d-flex">
				<div class="current-month-wrapper me-auto">
					<i class="bi bi-arrow-left"></i>
					<a class="current-month mx-1" id="current-month"></a>
					<i class="bi bi-arrow-right"></i>
				</div>

				<a class="about pe-2">Зачем?</a>
				<a class="my-music">Моя музыка</a>
			</div>

			<div class="calendar-carousel py-3 d-flex" id="calendar-carousel"></div>

			<div class="row">
				<div class="col-8">
					<div class="block daily-playlist my-3" id="daily-playlist">
						<p>Плейлист второго июля</p> 
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

		</div>




		<p>инфографика</p>
		<p>сначала за сегодняшний день, сколько песен из дневного плейлиста есть в моей музыке, сколько песен из него же есть в предыдущих плейлистах</p>
		<p>где-то нужно вывести график как с течением времени уменьшается количество уникальных песен в ежедневниках</p>

		<a>
			Расширение для браузера <i class="bi-github" role="img" aria-label="GitHub"></i>
		</a>
		<a>
			Api <i class="bi-github" role="img" aria-label="GitHub"></i>
		</a>
		<a>
			Front <i class="bi-github" role="img" aria-label="GitHub"></i>
		</a>
	</div>
</template>


<script>
export default {
	name: 'MainPage',
	props: {
		msg: String
	},
	data() {
		return {
			monthList: ['Январь', 'Февраль', 'Март', 'Апрель', 'Май', 'Июнь', 'Июль', 'Август', 'Сентябрь', 'Октябрь', 'Ноябрь', 'Декабрь'],
			getLastDailyPlaylist: 'http://localhost:1111/lastGetedPlaylist'
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
			
			for (let song in data.playlist) {
				document.getElementById('daily-playlist').append(this.addSong(song, data.playlist[song]))
			}
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
		displayCurrentPlaylist() {

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
	width: 100%; 
	border-radius: 12px;
	background: white;
}
.daily-playlist {
	overflow-y: auto;
	height: 400px;
}
.daily-playlist::-webkit-scrollbar {
	width: 5px;
}
.daily-playlist::-webkit-scrollbar-thumb {
	border-radius: 3px;
	background-color: #0077ff;
}
.about-daily-playlist {
	height: 400px;
}
.uniqueness-percent {
	background: #ffb366;
}
</style>
