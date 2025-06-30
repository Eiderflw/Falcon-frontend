<template>
	<div class="flex flex-column gap-2 relative z-2 posicion align-items-center relative">
		<img :class="`clasificacion pos-${tipo} z-1 relative`" :src="`/assets/img/fondo${tipo}.png`" alt="Top" />
		<img src="/assets/img/home/top/esfera_flotante.gif" alt="Top 3" class="z-1 absolute animacion top3 w-full" v-if="tipo == 'Cobre'" />
		<div class="contenedor-animacion w-full z-1 absolute" v-if="tipo == 'Oro'">
			<img src="/assets/img/home/top/llamas.gif" alt="Top 1" class="z-1 animacion relative top1 izquierda" />
			<img src="/assets/img/home/top/llamas.gif" alt="Top 1" class="z-1 animacion relative top1 derecha" />
		</div>
		<img src="/assets/img/home/top/velas.gif" alt="Top 2" class="z-1 absolute animacion top2" v-if="tipo == 'Platino'" />
		<img
			:src="foto == null || foto.length == 0 ? '/assets/img/avatar-default.jpg' : foto"
			:class="`imgProfile border-circle z-0 absolute pos-${tipo}`"
			alt="Foto"
		/>

		<div :class="`datos-personales pos-${tipo} relative`">
			<p class="m-0 text-center">{{ nombre }}</p>
		</div>
		<div :class="`info-destacada pos-${tipo} flex flex-column px-2 py-3`">
			<div class="insignias overflow-auto">
				<div class="title m-0 sticky top-0">
					<h2 class="w-full text-center m-0 text-black-alpha-90 text-lg uppercase">INSIGNIAS</h2>
				</div>
				<div class="flex w-full gap-1 flex-wrap pt-2 justify-content-center">
					<Avatar
						v-for="(insignia, index) in insignias"
						:key="index"
						:image="insignia.secure_url"
						v-tooltip.top="insignia.descripcion"
						size="large"
						shape="circle"
					/>
				</div>
			</div>
			<div class="grupo">
				<div class="title m-0">
					<h2 class="w-full text-center m-0 text-black-alpha-90 text-lg uppercase">GRUPO</h2>
				</div>
				<p class="font-bold text-md text-center">{{ grupo }}</p>
			</div>
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
		grupo: String,
		insignias: {
			type: Array,
			default: () => [],
		},
		mostrarNombre: {
			type: Boolean,
			default: true,
		},
	},
};
</script>
<style scoped>
.posicion > .info-destacada .title {
	color: black;
	background: #fff;
	border-radius: 8px;
	padding: 5px 10px;
}
.posicion > .info-destacada {
	height: 300px;
	width: 270px;
	backdrop-filter: blur(4px);
	box-shadow: 0px 4px 4px 0px #00000040;
	border-radius: 10px;
}
.posicion > .info-destacada > * {
	height: 50%;
}
.posicion > .animacion.top2 {
	height: 220px;
}
.posicion > .animacion {
	height: 150px;
	top: 85px;
}
.posicion > .contenedor-animacion {
	transform: rotate(90deg);
	margin-top: -15px;
}
.posicion > .contenedor-animacion .izquierda {
	transform: rotate(-25deg);
	bottom: -50px;
}
.posicion > .contenedor-animacion .derecha {
	transform: rotate(25deg);
	top: -50px;
}
.posicion > .contenedor-animacion > * {
	height: 300px;
	width: 400px;
}
.posicion > .info-destacada::before {
	content: "";
	position: absolute;
	inset: 0;
	border-radius: 10px;
	background: linear-gradient(180deg, #bf915c 0%, #f24949 100%) border-box;
	z-index: -1;
	border: 1.5px solid transparent;
	-webkit-mask: linear-gradient(#fff 0 0) padding-box, linear-gradient(#fff 0 0);
	-webkit-mask-composite: xor;
	mask-composite: exclude;
	pointer-events: none;
}
.posicion > .info-destacada.pos-Oro::before,
.posicion > .datos-personales.pos-Oro::before {
	background: linear-gradient(180deg, #5cadbf 0%, #4957f2 100%) border-box;
}

.posicion > .datos-personales {
	padding: 4px 9px;
	width: 150px;
	border-radius: 10px;
	text-shadow: 3px -1px 0px rgba(254, 44, 85, 1);
}
.posicion > .datos-personales.pos-Oro {
	text-shadow: 3px -1px 0px rgb(73, 87, 242);
}
.posicion > .datos-personales::before {
	content: "";
	position: absolute;
	inset: 0;
	border-radius: 10px;
	background: linear-gradient(90deg, #f24949 0%, #bf915c 100%) border-box;
	z-index: -1;
	border: 1px solid transparent;
	-webkit-mask: linear-gradient(#fff 0 0) padding-box, linear-gradient(#fff 0 0);
	-webkit-mask-composite: xor;
	mask-composite: exclude;
	pointer-events: none;
}

.clasificacion {
	width: 270px;
	height: 300px;
	background-size: contain;
	background-repeat: no-repeat;
}

.posicion > .imgProfile {
	width: 145px;
	height: 145px;
	top: 62px;
	left: calc(50% - 73px);
	user-select: none;
}
.posicion > .imgProfile.pos-Oro {
	width: 223px;
	height: 223px;
	top: 82px;
	left: 89px;
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
@media (max-width: 655px) {
	.posicion > .animacion.top2 {
		height: 200px !important;
	}
	.posicion > .animacion {
		height: 100px !important;
		top: 110px !important;
	}
	.posicion > .contenedor-animacion {
		margin-top: 140px !important;
	}
	.posicion > .contenedor-animacion > * {
		height: 200px !important;
		width: 300px !important;
	}
	.posicion > .contenedor-animacion .izquierda {
		bottom: 0 !important;
	}
	.posicion > .contenedor-animacion .derecha {
		top: 0 !important;
	}
}
@media (max-width: 518px) {
	.posicion > .contenedor-animacion {
		margin-top: 220px !important;
	}
	.posicion > .contenedor-animacion > * {
		height: 150px !important;
		width: 250px !important;
	}
	.posicion > .contenedor-animacion .izquierda {
		bottom: 0 !important;
	}
	.posicion > .contenedor-animacion .derecha {
		top: 0 !important;
	}
}
@media (max-width: 401px) {
	.clasificacion,
	.clasificacion.pos-Oro {
		width: 250px !important;
		height: 250px !important;
	}
	.posicion > .imgProfile {
		width: 130px !important;
		height: 130px !important;
		left: 69px !important;
		top: 59px !important;
	}
	.posicion > .imgProfile.pos-Oro {
		width: 140px !important;
		height: 140px !important;
		left: 65px !important;
		top: 52.1px !important;
	}

	.posicion > .contenedor-animacion {
		margin-top: 80px !important;
	}
	.posicion > .contenedor-animacion > * {
		height: 120px !important;
		width: 220px !important;
	}
}
@media (max-width: 330px) {
	.posicion > .contenedor-animacion {
		margin-top: 125px !important;
	}
	.posicion > .contenedor-animacion > * {
		height: 90px !important;
		width: 200px !important;
	}
}
</style>
