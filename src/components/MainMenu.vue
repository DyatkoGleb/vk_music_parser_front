<template>
	<div class="main-menu d-flex" id="main-menu">
        <div class="current-month-wrapper me-auto">
            <i class="bi bi-arrow-left"></i>
            <a class="current-month mx-1" id="current-month"></a>
            <i class="bi bi-arrow-right"></i>
        </div>

        <a class="about pe-2" @click="displayAboutNote">Зачем?</a>
        <a class="my-music">Моя музыка</a>
	</div>
</template>


<script>
export default {
	name: 'MainMenu',
    methods: {
        displayAboutNote() {
            this.emitter.emit('displayAboutNote')
        }
    }
}
</script>


<style>
.main-menu {
    position: relative;
    background: #edeef0;
    max-width: 1200px;
    width: 100%;
    margin: auto;
    padding: 20px 30px 20px 30px;
}
</style>
