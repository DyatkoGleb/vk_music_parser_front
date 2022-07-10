<template>
	<div class="calendar-carousel pb-4 d-flex" id="calendar-carousel"></div>
</template>


<script>
export default {
	name: 'CalendarCarousel',
	props: {
		playlistsProps: Object,
	},
    data() {
        return {
            playlists: {}
        }
    },
    methods: {
        allDateExistsPlaylists() {
            for (let playlist of this.playlists) {
                let playlistDate = new Date(playlist['date'])
                let a = document.createElement('a')

                a.classList.add('calendar-day')
                a.innerText = playlistDate.getDate()
                document.getElementById('calendar-carousel').append(a)
            }
        }
    },
    watch: {
     'playlistsProps': function(value) {
        this.playlists = value
        this.allDateExistsPlaylists()
     }
   }
}
</script>


<style>
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
</style>
