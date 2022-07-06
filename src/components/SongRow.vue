<template>
	<div class="song-row">
		{{ artist }} - {{ name }}
	</div>
	
</template>


<script>
export default {
	name: 'SongRow',
	props: {
		artist: String,
		name: String
	},
}
</script>


<style>
.song-row {
	padding: 8px;
	margin: 8px;
	border-radius: 5px;
	background: #edeef0;
	text-align: left;
	white-space: nowrap;
	overflow: hidden;
}
</style>
