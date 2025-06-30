<template>
	<section class="top-creadores flex flex-wrap row-gap-2 justify-content-center lg:justify-content-between relative">
		<video class="fondo w-full absolute" src="/assets/video/home/fondo_top_aliado_select.mp4" autoplay loop muted>
			<source src="/assets/video/home/fondo_top_aliado_select.mp4" type="video/mp4" />
			Tu navegador no soporta esta funcionalidad video
		</video>
		<div class="top-seleccionado relative">
			<div class="top-title px-2 py-2 font-monda">
				<h2 class="m-0 p-0 uppercase text-center text-xl">SELECCIONADO</h2>
			</div>
			<div class="flex flex-column gap-1">
				<div class="lista-creadores w-full flex flex-column gap-3 pt-3">
					<div
						v-for="(seleccionado, index) in topSeleccionado"
						:key="index"
						:class="`top-creador ${index == 0 ? 'top1' : 'top' + (index + 1)}`"
					>
						<div v-if="index == 0" class="item flex flex-column justify-content-center align-items-center">
							<div class="marco flex align-items-center justify-content-center relative">
								<div class="foto-top1 relative border-circle" v-if="seleccionado.foto == null || seleccionado.foto.trim().length == 0" />
								<Avatar v-else :image="seleccionado.foto" size="xlarge" class="foto-top1 relative" shape="circle" />
							</div>
							<p class="m-0 font-bold nombre-usuario font-monomaniac-one uppercase">{{ seleccionado.usuario }}</p>
							<div class="diamantes-top mt-2 flex gap-1 align-items-center flex-wrap justify-content-center relative">
								<Avatar image="/assets/img/home/diamante.gif" size="large" />
								<p class="m-0 font-bold text-3xl uppercase font-monomaniac-one">
									{{ seleccionado.diamantes_mes_actual.toLocaleString() }}
								</p>
							</div>
						</div>
						<div v-else class="item flex justify-content-between align-items-center">
							<div class="info-basica flex flex-wrap align-items-center gap-1">
								<p class="font-bold m-0 font-play-pretend-home">{{ (index + 1).toString().padStart(2, "0") }}</p>
								<Avatar :image="seleccionado.foto" size="large" class="avatar-tabla" shape="circle" />
								<p class="font-bold m-0">{{ seleccionado.usuario }}</p>
							</div>
							<div class="puntuacion flex flex-wrap gap-1 justify-content-center align-items-center">
								<strong>{{ seleccionado.diamantes_mes_actual.toLocaleString() }}</strong>
								<Avatar image="/assets/img/home/diamante.gif" class="avatar-tabla" size="large" />
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
		<div class="carousel h-max relative mt-6 p-4">
			<div class="titulo-videos w-max px-3 py-3 m-auto relative">
				<h2 class="m-0 uppercase text-center w-full text-2xl font-play-pretend-home">Batallas TikTok</h2>
			</div>
			<carousel-3d
				:autoplay="true"
				:width="widthSlide"
				:height="heightSlide"
				:border="0"
				:display="displaySlides"
				:count="slides.length"
				:autoplayHoverPause="true"
				:controlsVisible="true"
				:perspective="1"
				:startIndex="0"
				:loop="true"
				class="carousel-videos m-0 h-auto"
				@after-slide-change="pasarSlide"
				ref="carousel_videos"
			>
				<slide v-for="(slide, i) in slides" :index="i" :key="i">
					<video
						class="w-full h-full"
						:src="slide.url"
						style="object-fit: fill; object-position: center"
						:ref="`ref-video-${i}`"
						@click="pausarAnterior(null, false)"
						crossorigin="anonymous"
					>
						<source :src="slide.url" type="video/*" />
						Tu navegador no soporta videos HTML5
					</video>
					<div class="video-overlay z-3 transition-all transition-duration-200 transition-ease-in fadein animation-duration-1000 flex">
						<img src="/assets/img/play_button.svg" style="width: 100px !important" alt="Play" @click="reproducir" />
					</div>
				</slide>
			</carousel-3d>
			<div class="filtros w-full flex flex-wrap gap-3 mt-4 justify-content-center align-items-center">
				<button class="btn_filtro text-xl font-play-pretend-home uppercase" v-for="(f, index) in btn_filtros" :key="index">{{ f }}</button>
			</div>
		</div>

		<div class="top-agencias relative">
			<div class="top-title px-3 py-2 font-monda">
				<h2 class="m-0 p-0 uppercase text-center text-xl">ALIADO</h2>
			</div>
			<div class="flex flex-column gap-1">
				<div class="lista-creadores w-full flex flex-column gap-3 pt-3">
					<div
						v-for="(aliado, index) in topAliados"
						:key="index"
						:class="`top-creador ${aliado.agencia.toLowerCase().replaceAll(' ', '_')} ${index == 0 ? 'top1' : 'top' + (index + 1)}`"
					>
						<div v-if="index == 0" class="item flex flex-column justify-content-center align-items-center">
							<div class="marco flex align-items-center justify-content-center relative">
								<div class="foto-top1 relative border-circle" v-if="aliado.foto == null || aliado.foto.trim().length == 0" />
								<Avatar v-else :image="aliado.foto" size="xlarge" class="foto-top1 relative" shape="circle" />
							</div>
							<p class="m-0 font-bold nombre-usuario font-monomaniac-one uppercase">{{ aliado.usuario }}</p>
							<div class="diamantes-top mt-2 flex gap-1 align-items-center flex-wrap justify-content-center relative">
								<Avatar image="/assets/img/home/diamante.gif" size="large" />
								<p class="m-0 font-bold text-3xl uppercase font-monomaniac-one">
									{{ aliado.diamantes_mes_actual.toLocaleString() }}
								</p>
							</div>
						</div>
						<div v-else class="item flex justify-content-between align-items-center">
							<div class="info-basica flex flex-wrap align-items-center gap-1">
								<div class="avatar-tabla border-circle fondo-avatar-default" v-if="aliado.foto == null || aliado.foto.trim().length == 0" />
								<Avatar v-else :image="aliado.foto" size="large" class="avatar-tabla" shape="circle" />
								<p class="font-bold m-0 text-white">{{ aliado.usuario }}</p>
							</div>
							<div class="puntuacion flex flex-wrap gap-1 justify-content-center align-items-center">
								<strong class="text-white">{{ aliado.diamantes_mes_actual.toLocaleString() }}</strong>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>
</template>
<script>
import axios from "axios";
export default {
	data: () => ({
		API: import.meta.env.VITE_APP_API,
		btn_filtros: ["BATALLAS", "MOMENTOS", "PREMIOS"],
		topSeleccionado: [],
		topAliados: [],
		slides: [],
		current_index_slide: 0,
		last_index_slide: null,
		current_video: null,
		displaySlides: 1,
		widthSlide: 420,
		heightSlide: 300,
	}),
	methods: {
		mostrarSlide(index = 0) {
			this.$refs.carousel_videos.goSlide(index);
		},
		pasarSlide(index) {
			this.last_index_slide = this.current_index_slide;
			this.current_index_slide = index;
		},
		reproducir(ev) {
			const slider = ev.target.parentElement.parentElement;
			if (slider.childElementCount == 2) {
				const video = slider.firstChild.nextElementSibling;
				const overlay = slider.lastChild.previousElementSibling;
				if (overlay) {
					if (overlay.classList.contains("flex")) {
						overlay.classList.remove("flex");
						overlay.classList.add("hidden");
						video.play();
						video.onended = () => {
							video.currentTime = 0;
							overlay.classList.remove("hidden");
							overlay.classList.add("flex");
						};
					} else {
						overlay.classList.remove("hidden");
						overlay.classList.add("flex");
						video.pause();
					}
				}
			}
		},
		pausarAnterior(video = HTMLVideoElement, origin_watch = true) {
			//Si el origin_watch=true, viene del watch y video tiene el elemento html
			let container_slider, overlay;

			if (origin_watch) {
				container_slider = video.parentElement;
				overlay = container_slider.lastChild.previousElementSibling;
				video.pause();
				video.currentTime = 0;
				if (overlay.classList.contains("hidden")) {
					overlay.classList.remove("hidden");
					overlay.classList.add("flex");
				}
			} else {
				//Si el overlay está oculto, pauso el vídeo actual sino no hago nada, solo quiero pasar el slider
				video = this.$refs[`ref-video-${this.current_index_slide}`][0];
				container_slider = video.parentElement;
				overlay = container_slider.lastChild.previousElementSibling;
				if (overlay && overlay.classList.contains("hidden")) {
					video.pause();
					overlay.classList.remove("hidden");
					overlay.classList.add("flex");
				}
			}
		},
		calcularMedidasCarousel() {
			const widthVen = window.innerWidth;
			//Medidas para el carousel de videos
			if (widthVen > 700 && widthVen < 900) {
				this.widthSlide = 340;
				this.heightSlide = 270;
			} else if (widthVen >= 900 && widthVen <= 1280) {
				this.widthSlide = 400;
				this.heightSlide = 300;
			} else if (widthVen > 1280 && widthVen < 1440) {
				this.widthSlide = 430;
				this.heightSlide = 310;
			} else if (widthVen >= 1440 && widthVen < 2200) {
				this.widthSlide = 440;
				this.heightSlide = 310;
			} else if (widthVen >= 2200) {
				this.widthSlide = 480;
				this.heightSlide = 360;
			}

			if (widthVen <= 1024) {
				this.displaySlides = 3;
			} else if (widthVen > 1024 && widthVen < 1440) {
				this.displaySlides = 4;
			} else {
				this.displaySlides = 5;
			}
		},
	},
	watch: {
		last_index_slide(newValue) {
			const video = this.$refs[`ref-video-${newValue}`];
			if (video) {
				if (video.length == 1) {
					this.pausarAnterior(video[0]);
				}
			}
		},
	},
	async created() {
		await axios.get(`${this.API}/top-seleccionado`).then((r) => {
			this.topSeleccionado = Array.isArray(r.data.seleccionado) && r.data.seleccionado.length > 0 ? r.data.seleccionado : [];
		});
		await axios.get(`${this.API}/usuario/agencias/top10`).then((r) => {
			this.topAliados = r.data;
		});
		this.slides = [
			{ url: "https://res.cloudinary.com/dyo2vl0fx/video/upload/v1733002154/videosdestacados/yjsjfc0ywhtymiojclt8.mp4" },
			{ url: "https://res.cloudinary.com/dyo2vl0fx/video/upload/v1733002140/videosdestacados/rzwfwplhtygdvbd6kq9c.mp4" },
			{ url: "https://res.cloudinary.com/dyo2vl0fx/video/upload/v1733002136/videosdestacados/aktjptvgq3wbfndgkwgb.mp4" },
			{ url: "https://res.cloudinary.com/dyo2vl0fx/video/upload/v1733002135/videosdestacados/hsexksruxxtqlczahj4c.mp4" },
			{ url: "https://res.cloudinary.com/dyo2vl0fx/video/upload/v1733002135/videosdestacados/qsvfbu389m7tficerpax.mp4" },
			{ url: "https://res.cloudinary.com/dyo2vl0fx/video/upload/v1733002125/videosdestacados/kl1yevqrqk2hlhjf4dec.mp4" },
			{ url: "https://res.cloudinary.com/dyo2vl0fx/video/upload/v1733002119/videosdestacados/h6n9yf7ybpa37qys01rm.mp4" },
		];
	},
};
</script>
<style scoped>
.carousel-3d-slide {
	border-radius: 12px;
}
.indicator-slide {
	height: 18px;
	width: 18px;
	border: 2px solid #ffffff;
	background: transparent;
}

.indicator-slide.active {
	background-color: #ffffff;
}
.luz_top1 {
	position: absolute;
	right: -27px;
	top: -27px;
}
.top-agencias > .top-title,
.top-seleccionado > .top-title {
	background-color: #1e6572;
	color: white;
	top: 13px;
	width: 180px;
	position: absolute;
	left: calc(50% - 90px);
	line-height: 1;
	border-radius: 10px;
	margin: 0 auto;
	box-shadow: 0px 3px 12px 5px rgba(30, 101, 114, 0.6);
	-webkit-box-shadow: 0px 3px 12px 5px rgba(30, 101, 114, 0.6);
	-moz-box-shadow: 0px 3px 12px 5px rgba(30, 101, 114, 0.6);
}
.titulo-videos {
	background: url("/assets/img/btn_title_batalla.png");
	background-repeat: no-repeat;
	background-size: 100% 100%;
	height: 70px;
	max-width: 700px;
	z-index: 5;
	top: -59px;
}
.video-overlay {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	display: flex;
	align-items: center;
	justify-content: center;
	width: 100%;
	height: 100%;
	background-color: rgba(0, 0, 0, 0.4);
	color: #ffffff;
	font-size: 36px;
	font-weight: bold;
	cursor: pointer;
}
.top-creadores {
	background-repeat: no-repeat;
	min-height: 1042px !important;
}
.top-creadores > .fondo {
	z-index: 0;
	object-fit: contain;
}
.top-creadores > .top-seleccionado,
.top-creadores > .top-agencias {
	background-image: url("/assets/img/home/top/marco_top.gif");
	background-repeat: no-repeat;
	background-position: top;
	background-size: 100% 100%;
	padding: 45px 45px 50px 47px;
	width: 450px;
	min-width: 400px;
	height: 928px;
	max-height: 950px;
	z-index: 1;
}
.top-creadores > .top-seleccionado > div > .lista-creadores,
.top-creadores > .top-agencias > div > .lista-creadores {
	border: none;
	border-image: linear-gradient(180deg, #1d2235 0%, #121318 100%);
	background-image: url("/assets/img/home/top/fondo.png");
	background-repeat: no-repeat;
	background-size: 100% 100%;
	background-position: top;
	height: 830px;
	max-height: 850px;
	overflow: auto;
	padding: 0 4px 4px 4px;
	box-shadow: 0px 11.81px 53.15px 0px #00000059;
}
.lista-creadores > .top-creador.top1 > .item > .marco {
	background-image: url("/assets/img/home/top/marco_top1.gif");
	background-repeat: no-repeat;
	background-size: 100% 100%;
	height: 150px;
	width: 150px;
}
.lista-creadores > .top-creador.top1 > .item > .marco > * {
	height: 113px;
	width: 113px;
	background-color: #3c0806;
}
.lista-creadores > .top-creador.top1 > .item > .nombre-usuario {
	background: #ffffff66;
	color: #000000;
	padding: 2px 10px;
	box-shadow: 0px 8px 4px 0px #00000040;
	-webkit-box-shadow: 0px 8px 4px 0px #00000040;
	-moz-box-shadow: 0px 8px 4px 0px #00000040;
	border-radius: 8px;
}
.lista-creadores > .top-creador:not(.top1) {
	padding: 4px 6px;
	border-radius: 12px;
	background-color: #264157;
}
.fondo-avatar-default {
	background-color: #5cadbf;
}
.btn_filtro {
	width: max-content;
	padding: 5px 16px;
	text-transform: uppercase;
	border-radius: 8px;
	font-weight: bold;
	cursor: pointer;
	z-index: 2;
	background-color: #b5a152;
	border: 1px solid;
	border-image-source: linear-gradient(180deg, #6c8c7c 0%, #314a4d 100%);
	box-shadow: 4px -4px 9.8px 2px #1e6572b5;
	-webkit-box-shadow: 4px -4px 9.8px 2px #1e6572b5;
	-moz-box-shadow: 4px -4px 9.8px 2px #1e6572b5;
	color: #470808;
	font-family: "Monomaniac-One";
}

.btn_filtro:focus {
	border: 2px solid #1e6572b5;
}
.top-creadores > .carousel {
	background-color: #1e1c1d;
	z-index: 2;
	border-radius: 8px;
}

@media (min-width: 900px) {
	.top-creadores > .carousel {
		width: calc(100% - 300px) !important;
	}
}

@media (min-width: 2200px) {
	.top-creadores > .carousel {
		width: 40% !important;
	}
	.top-creadores > .carousel > .carousel-videos {
		width: 100% !important;
	}
}

@media (min-width: 1200px) {
	.top-creadores {
		justify-content: space-between !important;
	}
	.top-creadores > .carousel {
		width: calc(100% - 600px) !important;
	}
}

@media (min-width: 1500px) {
	.top-creadores {
		justify-content: space-evenly !important;
	}
	.top-creadores > .carousel {
		width: calc(100% - 990px) !important;
	}
}
@media (max-width: 1500px) {
	.carousel {
		width: 90% !important;
	}
	.top-creadores {
		justify-content: center !important;
		height: 1700px !important;
	}
	.top-creadores > .fondo {
		height: 1700px !important;
		object-fit: fill !important;
	}
	.top-creadores > .top-seleccionado {
		order: 0;
	}
	.top-creadores > .top-agencias {
		order: 1;
	}
	.top-creadores > .carousel {
		order: 2;
	}
}
@media (max-width: 900px) {
	.top-creadores,
	.top-creadores > .fondo {
		height: 2800px !important;
	}
}
@media (max-width: 420px) {
	.top-creadores > .top-seleccionado,
	.top-creadores > .top-agencias {
		padding: 46px 41px 50px 42px;
	}
}
@media (max-width: 400px) {
	.top-creadores > .top-seleccionado,
	.top-creadores > .top-agencias {
		min-width: 250px;
	}
}

@media (max-width: 390px) {
	.top-creadores > .top-seleccionado,
	.top-creadores > .top-agencias {
		padding: 45px 39px 48px 40px;
	}
}
@media (max-width: 360px) {
	.top-creadores > .top-seleccionado,
	.top-creadores > .top-agencias {
		padding: 47px 35px 49px 37px;
	}
}

@media (max-width: 355px) {
	.top-creadores > .top-seleccionado,
	.top-creadores > .top-agencias {
		min-width: 100%;
		height: 950px;
		padding: 47px 34px 50px 36px;
	}
	.top-creadores > .top-seleccionado > div > .lista-creadores,
	.top-creadores > .top-agencias > div > .lista-creadores {
		height: 850px;
		max-height: 870px;
	}
	.carousel {
		width: 99% !important;
	}
	.titulo-videos {
		left: calc(50% - 140px);
	}
}

@media (max-width: 318px) {
	.top-creadores > .top-seleccionado,
	.top-creadores > .top-agencias {
		padding: 47px 31px 50px 32px;
		height: 1020px;
		max-height: 1500px;
	}
	.top-creadores > .top-seleccionado > div > .lista-creadores,
	.top-creadores > .top-agencias > div > .lista-creadores {
		max-height: 1000px;
		height: 917px;
	}
}
</style>