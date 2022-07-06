<template>
	<div class="main-menu" id="main-menu">
        <div class="d-flex nav">
            <div class="current-month-wrapper me-auto">
                <i class="bi bi-arrow-left"></i>
                <a class="current-month mx-1" id="current-month"></a>
                <i class="bi bi-arrow-right"></i>
            </div>

            <a class="about pe-2">Зачем?</a>
            <a class="my-music">Моя музыка</a>
        </div>
	</div>

</template>


<script>
export default {
	name: 'MainMenu'
}
</script>


<style>
.main-menu {
    position: relative;
    width: 100%;
    background: #edeef0;
}
.nav {
    max-width: 1140px;
    width: 100%;
    margin: auto;
    padding: 20px 0;
}
</style>
