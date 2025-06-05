<template>
	<div :class="`clasificacion pos-${tipo}`">
		<img class="imgFondo" :src="`/assets/img/fondo${tipo}.png`" alt="" />
		<img :src="foto" class="imgProfile" alt="" />
		<div class="labelNombre" v-if="mostrarNombre">
			<p class="m-0 font-gamers">{{ nombre }}</p>
		</div>
	</div>
</template>
<script>
export default {
	props: {
		tipo: String,
		foto: String,
		nombre: String,
		top: String,
		mostrarNombre: {
			type: Boolean,
			default: true,
		},
	},
};
</script>
<style scoped>
.clasificacion {
	width: 270px;
	height: 300px;
	display: flex;
	justify-content: center;
	flex-direction: column;
	align-items: center;
}

.clasificacion > .imgEtiqueta {
	position: relative;
	z-index: 3;
}

.clasificacion > .imgProfile {
	position: relative;
	width: 135px;
	height: 135px;
	border-radius: 50%;
	z-index: 2;
	top: 13px;
}

.clasificacion > .imgFondo {
	position: absolute;
}
.clasificacion.pos-OroPequeno,
.clasificacion.pos-PlatinoPequeno,
.clasificacion.pos-CobrePequeno,
.clasificacion.pos-OroPequeno > .imgFondo,
.clasificacion.pos-PlatinoPequeno > .imgFondo,
.clasificacion.pos-CobrePequeno > .imgFondo {
	width: 79px !important;
	height: 79px !important;
	max-width: 79px;
	max-height: 79px;
	display: block;
}

.clasificacion.pos-OroPequeno > .imgProfile,
.clasificacion.pos-PlatinoPequeno > .imgProfile,
.clasificacion.pos-CobrePequeno > .imgProfile {
	width: 41px !important;
	height: 41px !important;
	top: 0;
	margin: 17px 0 19px 20px;
}

.Oro {
	background-color: #fbd05b;
}

.Platino {
	background-color: #b4d0f8;
}

.Cobre {
	background-color: #9b5e13;
}

.clasificacion > .labelNombre {
	top: 68px;
	position: relative;
	z-index: 2;
	display: flex;
	justify-content: center;
}

.badgeDiv {
	position: relative;
	top: 66px;
	z-index: 5;
	display: flex;
	justify-content: center;
}
</style>
<style>
@media (max-width: 400px) {
	.clasificacion.pos-Oro {
		width: 100% !important;
	}
}
</style>
<style>
</style>
