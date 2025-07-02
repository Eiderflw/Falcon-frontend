<template>
	<div class="home">
		<NavBar />
		<div class="inicio">
			<div class="fondo">
				<div class="destacado" id="destacado">
					<video src="/assets/video/home/fondo_top_categorias.mp4" autoplay loop>
						<source src="/assets/video/home/fondo_top_categorias.mp4" type="video/mp4" />
						Tu navegador no soporta esta funcionalidad video
					</video>
					<div class="flex flex-wrap gap-6 top">
						<div class="foto relative">
							<img class="marco_foto" src="/assets/img/home/marco-foto.png" alt="Marco foto" />
							<img src="/assets/img/home/aura.gif" alt="Aura foto" class="aura_foto" />
							<img :src="topDestacado.foto.length == 0 ? '/assets/img/avatar-default.jpg' : topDestacado.foto"
								alt="Top 1"
								class="top_destacado transition-all transition-duration-1000 fadein animation-duration-1000" />
							<span class="descripcion_destacado absolute text-center bg-black-alpha-90 font-bold">{{
								descripcion_destacado }}</span>
						</div>
						<div class="info flex flex-column">
							<div class="personal relative">
								<div class="nombre absolute text-center">{{ topDestacado.usuario }}</div>
								<div class="columnas flex flex-wrap w-100 justify-content-evenly font-metal-mania">
									<h2 class="m-0 p-0">DIAMANTES</h2>
									<h2 class="m-0 p-0">CATEGORÍA</h2>
								</div>
							</div>
							<div class="datos flex flex-wrap justify-content-evenly xl:justify-content-around">
								<div class="diamantes flex flex-column align-items-center flex-wrap">
									<img src="/assets/img/home/diamante.gif" alt="Diamante" class="diamante" />
									<p
										class="m-0 text-2xl text-center font-bold transition-all transition-duration-1000 fadein animation-duration-1000">
										{{ topDestacado.diamantes_mes_actual.toLocaleString() }}
									</p>
								</div>
								<div class="categoria flex flex-column align-items-center flex-wrap">
									<img src="/assets/img/home/insignia.gif" alt="Insignia" class="insignia" />
									<p
										class="m-0 text-2xl text-center font-bold transition-all transition-duration-1000 fadein animation-duration-1000 uppercase">
										{{ topDestacado.categoria }}
									</p>
								</div>
							</div>
						</div>
					</div>
				</div>
				<TopsCarouselVideos />
				<section id="unete"
					class="unete text-center flex flex-wrap justify-content-center gap-4 align-items-center">
					<div class="flex flex-column align-items-center gap-2">
						<h1 class="text-6xl m-0 font-mouse-memoirs uppercase">¡ANÍMATE!</h1>
						<h3 class="font-bold m-0 uppercase font-monomaniac-one">ATRÉVETE A SER PARTE DE ESTA FAMILIA
						</h3>
					</div>
					<a href="https://api.whatsapp.com/send?phone=50371976020" target="_blank"
						class="link_whatsapp relative transition-all fadein animation-duration-1000 uppercase no-underline text-white-alpha-90">
						<img src="/assets/img/btn_whatsapp.png" class="img_btn_escribenos" alt="Botón WhatsApp" />
					</a>
				</section>
				<CarouselNovedades />
				<Phone />
				<section id="clasificados" class="clasificados_destacados w-full relative">
					<video src="/assets/video/home/fondo_top3.mp4" class="absolute w-full" autoplay loop>
						<source src="/assets/video/home/fondo_top3.mp4" type="video/mp4" />
					</video>
					<div class="containerC py-5 align-items-start" v-if="clasificados.length > 2">
						<Clasificacion :nombre="clasificados[2].usuario" :grupo="clasificados[2].grupo"
							:insignias="clasificados[2].insignias" top="3" tipo="Cobre" :foto="clasificados[2].foto" />
						<Clasificacion top="1" tipo="Oro" :nombre="clasificados[0].usuario"
							:insignias="clasificados[0].insignias" :grupo="clasificados[0].grupo"
							:foto="clasificados[0].foto" />
						<Clasificacion :nombre="clasificados[1].usuario" top="2" :insignias="clasificados[1].insignias"
							:grupo="clasificados[1].grupo" tipo="Platino" :foto="clasificados[1].foto" />
					</div>
				</section>
				<CarouselResenas />
			</div>
		</div>
		<Footer id="footer" />
	</div>
</template>
<script>
import axios from "axios";

export default {
	data: () => ({
		API: import.meta.env.VITE_APP_API,
		clasificados: [
			{
				usuario: "x",
				foto: "",
				grupo: "",
				insignias: [],
			},
			{
				usuario: "x",
				foto: "",
				grupo: "",
				insignias: [],
			},
			{
				usuario: "x",
				foto: "",
				grupo: "",
				insignias: [],
			},
		],
		top5Diamantes: [],
		topDiamantesCategorias: [],
		indexTopDestacado: 0,
		indexTopCategoria: 0,
		topDestacadoTitle: "Diamantes",
		idIntervalDestacado: null,
		topDestacado: {
			categoria: "VETERAn",
			diamantes_mes_actual: 0,
			foto: "",
			usuario: "Sin usuario",
		},
		descripcion_destacado: "Top 1",
		top3: [
			{
				usuario: "x",
				foto: "/assets/img/perfil1.jpg",
				categoria: "",
				diamantes_mes_actual: 0,
				grupo: "",
			},
			{
				usuario: "x",
				foto: "",
				categoria: "",
				diamantes_mes_actual: 0,
				grupo: "",
			},
			{
				usuario: "x",
				foto: "",
				categoria: "",
				diamantes_mes_actual: 0,
				grupo: "",
			},
		],
	}),
	methods: {
		mostrarTopDestacado() {
			this.idIntervalDestacado = setInterval(() => {
				//Top5 diamates
				if (this.indexTopDestacado <= this.top5Diamantes.length - 1 && this.topDestacadoTitle == "Diamantes") {
					this.topDestacado.diamantes_mes_actual = this.top5Diamantes[this.indexTopDestacado].diamantes_mes_actual;
					this.topDestacado.foto = this.top5Diamantes[this.indexTopDestacado].foto;
					this.topDestacado.categoria = this.top5Diamantes[this.indexTopDestacado].creator_type;
					this.topDestacado.usuario = this.top5Diamantes[this.indexTopDestacado].usuario;
					this.descripcion_destacado = `Top ${this.indexTopDestacado + 1}`;
					this.indexTopDestacado++;

					if (this.indexTopDestacado > this.top5Diamantes.length - 1) {
						this.indexTopDestacado = 0;
						this.topDestacadoTitle = "Categorías";
					}
				} else if (this.topDestacadoTitle == "Categorías") {
					if (this.indexTopDestacado <= this.topDiamantesCategorias.length - 1) {
						const categoria = this.topDiamantesCategorias[this.indexTopDestacado];
						if (this.indexTopCategoria <= categoria.usuarios.length - 1) {
							this.topDestacado.diamantes_mes_actual = categoria.usuarios[this.indexTopCategoria].diamantes_mes_actual;
							this.topDestacado.foto = categoria.usuarios[this.indexTopCategoria].foto;
							this.topDestacado.categoria = categoria.usuarios[this.indexTopCategoria].creator_type;
							this.topDestacado.usuario = categoria.usuarios[this.indexTopCategoria].usuario;
							this.descripcion_destacado = `${categoria._id} ${this.indexTopCategoria + 1}`;
							this.indexTopCategoria++;
							if (this.indexTopCategoria > categoria.usuarios.length - 1) {
								this.indexTopCategoria = 0;
								this.indexTopDestacado++;
							}
						}
						if (this.indexTopDestacado > this.topDiamantesCategorias.length - 1) {
							this.topDestacadoTitle = "Diamantes";
							this.indexTopDestacado = 0;
						}
					}
				}
			}, 2800);
		},
	},
	async created() {
		//Obtener 10 mejores por diamantes, se cortan 5 primeros
		await axios.get(`${this.API}/usuario/diamantes/top10`).then((resp) => {
			this.top5Diamantes = resp.data.slice(0, 5);
		});
		//Primero se muestran los top5 de diamantes
		this.mostrarTopDestacado();
		//Obtenemos los 5 mejores de cada categoría
		await axios.get(`${this.API}/usuario/top5/categoria`).then((resp) => {
			this.topDiamantesCategorias = resp.data;
		});

		await axios.get(`${this.API}/usuario/top`).then((resp) => {
			if (resp.data.length > 0) {
				const usuarios = resp.data.flatMap((grupo) => grupo.usuarios);
				usuarios.sort((a, b) => b.diamantes_mes_actual - a.diamantes_mes_actual);

				this.top3[0].foto = usuarios[0].foto;
				this.top3[0].usuario = usuarios[0].usuario;
				this.top3[0].categoria = usuarios[0].creator_type;
				this.top3[0].diamantes_mes_actual = usuarios[0].diamantes_mes_actual;
				this.top3[0].grupo = usuarios[0].grupo;

				this.top3[1].foto = usuarios[1].foto;
				this.top3[1].usuario = usuarios[1].usuario;
				this.top3[1].categoria = usuarios[1].creator_type;
				this.top3[1].diamantes_mes_actual = usuarios[1].diamantes_mes_actual;
				this.top3[1].grupo = usuarios[1].grupo;

				this.top3[2].foto = usuarios[2].foto;
				this.top3[2].usuario = usuarios[2].usuario;
				this.top3[2].categoria = usuarios[2].creator_type;
				this.top3[2].diamantes_mes_actual = usuarios[2].diamantes_mes_actual;
				this.top3[2].grupo = usuarios[2].grupo;
			}
		});

		await axios.get(`${this.API}/usuario/homeCreadores`).then((resp) => {
			this.clasificados = resp.data.length == 0 ? this.clasificados : resp.data;
		});
	},
	unmounted() {
		clearInterval(this.idIntervalDestacado);
	},
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Lato&family=Raleway&display=swap");
@import url("https://fonts.googleapis.com/css?family=Playfair+Display:400,900");

body,
html {
	margin: 0;
	padding: 0;
	min-height: 100vh;
	background: #5cadbf;
	background: linear-gradient(85deg, rgba(92, 173, 191, 0.85) 30%, rgba(47, 70, 89, 0.78) 70%);
	box-sizing: border-box;
	scroll-behavior: smooth !important;
}

.home {
	background: #5cadbf;
	background: linear-gradient(85deg, rgba(92, 173, 191, 0.85) 30%, rgba(47, 70, 89, 0.78) 70%);
}

.destacado {
	width: 100%;
	height: 700px;
}

.destacado>* {
	width: 100%;
	height: 100%;
	object-fit: contain;
	object-position: top;
}

.descripcion_destacado {
	text-shadow: 2px 2px 9px white;
	width: 97px;
	height: 44px;
	left: calc(50% - 49px);
	bottom: 65px;
	z-index: 2;
	padding: 6px 7px 4px 7px;
}

.destacado>.categoria>div {
	pointer-events: none;
	background-repeat: no-repeat;
	background-position: top;
	background-size: 100% 100%;
	object-fit: contain;
	height: 54px;
	width: 340px;
	margin: 0;
}

.destacado>video {
	min-height: 540px;
	height: 100%;
	object-fit: cover;
	max-height: 700px;
}

.destacado>.top {
	position: absolute;
	display: flex;
	justify-content: center;
	align-items: center;
	top: 137px;
}

.destacado>.top>.foto>img.marco_foto {
	object-fit: contain;
	background-size: contain;
	background-repeat: no-repeat;
	width: 400px;
	height: 400px;
	position: relative;
	z-index: 3;
	user-select: none;
}

.destacado>.top>.foto>img.top_destacado {
	position: absolute;
	border-radius: 50%;
	top: calc(50% - 77px);
	left: calc(50% - 67px);
	width: 140px;
	height: 140px;
	z-index: 1;
}

.destacado>.top>.foto>img.aura_foto {
	position: absolute;
	border-radius: 50%;
	top: calc(50% - 164px);
	left: calc(50% - 214px);
	width: 432px;
	height: 320px;
	z-index: 2;
	user-select: none;
}

.destacado>.top>.info {
	min-width: 400px;
	height: min-content;
	padding: 6px 10px;
}

.destacado>.top>.info>.personal {
	background: radial-gradient(98.05% 261.61% at 1.95% 3.59%, rgba(255, 255, 255, 0.4) 0%, rgba(255, 255, 255, 0) 100%);
	padding: 14px 4px 2px 4px;
	border-width: 3px;
	border-style: solid;
	border-radius: 10px;
	/* Para bordes redondeados con border-image, usa un pseudo-elemento para simular el borde */
	position: relative;
	z-index: 1;
	border: none;
}

.destacado>.top>.info>.personal::before {
	content: "";
	position: absolute;
	inset: 0;
	border-radius: 10px;
	padding: 0;
	z-index: -1;
	border: 1.9px solid transparent;
	background: linear-gradient(90deg, #1e6572b5 0%, #5cadbf 100%) border-box;
	-webkit-mask: linear-gradient(#fff 0 0) padding-box, linear-gradient(#fff 0 0);
	-webkit-mask-composite: xor;
	mask-composite: exclude;
	pointer-events: none;
}

.destacado>.top>.info>.personal>.nombre {
	background-color: #1e6572;
	color: white;
	width: 150px;
	left: calc(50% - 75px);
	top: -22px;
	padding: 10px 2px;
	height: 40px;
	border-radius: 10px;
	margin: 0 auto;
	box-shadow: 0px 3px 12px 5px rgba(30, 101, 114, 0.6);
	-webkit-box-shadow: 0px 3px 12px 5px rgba(30, 101, 114, 0.6);
	-moz-box-shadow: 0px 3px 12px 5px rgba(30, 101, 114, 0.6);
}

.destacado>.top>.info>.personal>.columnas,
.destacado>.top>.info>.datos {
	text-shadow: 0px 2px 3px rgba(92, 173, 191, 1);
}

.destacado>.top>.info>.datos>.categoria>img.insignia {
	width: 65px;
	height: 65px;
}

.destacado>.top>.info>.datos>.diamantes {
	gap: 15px;
}

.home .unete {
	padding: 5rem 1rem;
}

.img_btn_escribenos {
	width: 130px;
	height: 130px;
}

.clasificados_destacados>video,
.clasificados_destacados {
	object-fit: cover;
	height: 900px;
}

.container {
	--bs-gutter-x: 1.5rem;
	--bs-gutter-y: 0;
	width: 100%;
	padding-right: calc(var(--bs-gutter-x) * 0.5);
	padding-left: calc(var(--bs-gutter-x) * 0.5);
	margin-right: auto;
	margin-left: auto;
}

.position-relative {
	position: relative !important;
}

.row {
	--bs-gutter-x: 1.5rem;
	--bs-gutter-y: 0;
	display: flex;
	flex-wrap: wrap;
	margin-top: calc(-1 * var(--bs-gutter-y));
	margin-right: calc(-0.5 * var(--bs-gutter-x));
	margin-left: calc(-0.5 * var(--bs-gutter-x));
}

.row>* {
	flex-shrink: 0;
	width: 100%;
	max-width: 100%;
	padding-right: calc(var(--bs-gutter-x) * 0.5);
	padding-left: calc(var(--bs-gutter-x) * 0.5);
	margin-top: var(--bs-gutter-y);
}

@media (min-width: 992px) {
	.col-lg-6 {
		flex: 0 0 auto;
		width: 50%;
	}

	.col-lg-3 {
		flex: 0 0 auto;
		width: 25%;
	}
}

@media (max-width: 940px) {
	.clasificados_destacados>.containerC {
		flex-direction: column !important;
		align-items: center !important;
	}

	.clasificados_destacados>.containerC .posicion:nth-child(odd) {
		margin-top: 0;
	}

	.clasificados_destacados>video,
	.clasificados_destacados {
		height: 2400px;
		object-fit: cover;
	}
}

@media (max-width: 659px) {
	.clasificados_destacados {
		padding: 0 !important;
	}
}

.fecha {
	background: transparent !important;
	border: 2px solid white;
	text-wrap: nowrap;
	width: max-content;
	border-radius: 50px;
	padding: 4px 8px;
}
</style>
<style>
body,
html {
	scroll-behavior: smooth !important;
}

.avatar-tabla {
	width: 40px !important;
	height: 40px !important;
}

.clasificados_destacados>.containerC .posicion:nth-child(odd) {
	margin-top: 190px;
}

@media (max-width: 1263px) {
	.destacado>.top>img.top_destacado {
		width: 178px !important;
		height: 178px !important;
		left: calc(50% - 90px) !important;
	}

	.destacado>.top>.username {
		bottom: -72px !important;
	}
}

@media (max-width: 1240px) {
	.destacado>.top>img.top_destacado {
		width: 176px !important;
		height: 176px !important;
		left: calc(50% - 89px) !important;
	}

	.destacado>.top>.username {
		bottom: -68px !important;
	}
}

@media (max-width: 1213px) {
	.destacado>.top>.username {
		bottom: -64px !important;
	}
}

@media (max-width: 1185px) {
	.destacado>.top>img.top_destacado {
		width: 167px !important;
		height: 167px !important;
		left: calc(50% - 85px) !important;
		top: 98px !important;
	}

	.destacado>.top>.username {
		bottom: -59px !important;
	}
}

@media (max-width: 1170px) {
	.destacado>.top>.username {
		bottom: -53px !important;
	}
}

@media (max-width: 1125px) {
	.destacado>.top>img.top_destacado {
		width: 158px !important;
		height: 158px !important;
		left: calc(50% - 79px) !important;
		top: 100px !important;
	}

	.destacado>.top>.username {
		bottom: -51px !important;
		font-size: 22px !important;
	}
}

@media (max-width: 1077px) {

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 300px;
	}

	.destacado>.top>.username {
		bottom: -62px !important;
	}
}

@media (max-width: 1051px) {
	.destacado>.top>img.top_destacado {
		width: 166px !important;
		height: 166px !important;
		left: calc(50% - 84px) !important;
		top: 98px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 460px) !important;
	}

	.destacado>.top>.username {
		bottom: -57px !important;
	}
}

@media (max-width: 1024px) {
	.destacado>.top>img.top_destacado {
		width: 162px !important;
		height: 162px !important;
		left: calc(50% - 82px) !important;
		top: 99px !important;
	}

	.destacado>.top>.username {
		bottom: -53px !important;
	}
}

@media (max-width: 998px) {
	.destacado>.top>img.top_destacado {
		width: 158px !important;
		height: 158px !important;
		left: calc(50% - 80px) !important;
		top: 100px !important;
	}

	.destacado>.top>.username {
		bottom: -49px !important;
	}
}

@media (max-width: 984px) {

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 280px !important;
	}

	.destacado>.top>img.top_destacado {
		width: 156px !important;
		height: 156px !important;
		left: calc(50% - 78px) !important;
		top: 100px !important;
	}

	.destacado>.top>.username {
		bottom: -47px !important;
	}
}

@media (max-width: 970px) {

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 250px !important;
	}

	.destacado>.top>.username {
		bottom: -44px !important;
	}
}

@media (max-width: 948px) {
	.destacado>.top>img.top_destacado {
		width: 149px !important;
		height: 149px !important;
		left: calc(50% - 76px) !important;
		top: 102px !important;
	}

	.destacado>.top>.username {
		bottom: -40px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 415px) !important;
	}

	.destacado>.diamantes,
	.destacado>.categoria {
		top: 250px !important;
	}
}

@media (max-width: 929px) {
	.destacado>video {
		object-fit: cover !important;
	}

	.destacado>.top>img.top_destacado {
		width: 149px !important;
		height: 149px !important;
		left: calc(50% - 76px) !important;
		top: 102px !important;
	}

	.destacado>.top>.username {
		bottom: -36px !important;
		font-size: 20px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 398px) !important;
	}

	.destacado>.diamantes,
	.destacado>.categoria {
		top: 260px !important;
	}
}

@media (max-width: 900px) {
	.destacado>.top>img.fondo {
		width: 98% !important;
	}

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 250px !important;
	}

	.destacado>.top>.username {
		bottom: -44px !important;
	}

	.destacado>.top>img.top_destacado {
		width: 153px !important;
		height: 153px !important;
		left: calc(50% - 77px) !important;
		top: 102px !important;
	}
}

@media (max-width: 878px) {
	.destacado>.top>img.top_destacado {
		left: calc(50% - 75px) !important;
		width: 150px !important;
		height: 150px !important;
	}

	.destacado>.top>.username {
		bottom: -41px !important;
	}

	.destacado>.categoria {
		right: 9%;
	}
}

@media (max-width: 860px) {
	.destacado>.top>img.top_destacado {
		top: 103px !important;
		left: calc(50% - 73px) !important;
		width: 145px !important;
		height: 145px !important;
	}

	.destacado>.top>.username {
		bottom: -35px !important;
	}

	.destacado>.categoria {
		left: calc(50% + 124px) !important;
	}
}

@media (max-width: 850px) {
	.destacado>video {
		height: 920px;
		max-height: 1000px;
	}

	.destacado {
		min-height: 840px;
		max-height: 840x;
	}
}

@media (max-width: 825px) {
	.destacado>.top>img.top_destacado {
		top: 104px !important;
		left: calc(50% - 71px) !important;
		width: 140px !important;
		height: 140px !important;
	}

	.destacado>.top>.username {
		bottom: -31px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 382px) !important;
	}

	.destacado>.categoria {
		left: calc(50% + 118px) !important;
	}
}

@media (max-width: 809px) {
	.destacado>.top>img.top_destacado {
		top: 105px !important;
		left: calc(50% - 70px) !important;
		width: 137px !important;
		height: 137px !important;
	}

	.destacado>.top>.username {
		bottom: -28px !important;
	}

	.clasificados_destacados>.borde_tabla {
		width: 650px !important;
		height: 2000px !important;
	}
}

@media (max-width: 795px) {
	.destacado>.top>img.top_destacado {
		top: 106px !important;
		left: calc(50% - 68px) !important;
		width: 135px !important;
		height: 135px !important;
	}

	.destacado>.top>.username {
		bottom: -25px !important;
		font-size: 18px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 367px) !important;
	}

	.destacado>.categoria {
		left: calc(50% + 100px) !important;
	}
}

@media (max-width: 782px) {
	.destacado>.top>img.top_destacado {
		top: 106px !important;
		left: calc(50% - 67px) !important;
		width: 132px !important;
		height: 132px !important;
	}

	.destacado>.diamantes>.title>.animacion,
	.destacado>.categoria>div>.animacion {
		object-fit: fill !important;
	}

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 230px !important;
		height: 50px !important;
	}

	.destacado>.top>.username {
		bottom: -21px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 367px) !important;
	}

	.destacado>.categoria {
		left: calc(50% + 115px) !important;
	}
}

@media (max-width: 760px) {
	.destacado>.top>.username {
		bottom: -16px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 350px) !important;
	}

	.destacado>.categoria {
		left: calc(50% + 115px) !important;
	}
}

@media (max-width: 750px) {

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 200px !important;
		height: 45px !important;
	}

	.destacado>.diamantes,
	.destacado>.categoria {
		top: 264px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 335px) !important;
	}

	.destacado>.top>img.top_destacado {
		width: 130px !important;
		height: 130px !important;
		left: calc(50% - 65px) !important;
		top: 106px !important;
	}

	.destacado>.top>.username {
		bottom: -15px !important;
	}
}

@media (max-width: 732px) {
	.destacado>.top>img.top_destacado {
		width: 130px !important;
		height: 130px !important;
		left: calc(50% - 65px) !important;
		top: 105px !important;
	}

	.destacado>.top>.username {
		bottom: -13px !important;
	}
}

@media (max-width: 721px) {
	.destacado>.top>img.top_destacado {
		width: 128px !important;
		height: 128px !important;
		left: calc(50% - 65px) !important;
		top: 105px !important;
	}

	.destacado>.top>.username {
		bottom: -9px !important;
	}
}

@media (max-width: 700px) {
	.destacado>.categoria {
		left: calc(50% + 105px) !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 313px) !important;
	}

	.destacado>.top>img.top_destacado {
		width: 125px !important;
		height: 125px !important;
		left: calc(50% - 63px) !important;
		top: 106px !important;
	}

	.destacado>.top>.username {
		bottom: -6px !important;
	}
}

@media (max-width: 686px) {
	.destacado>.top>img.top_destacado {
		width: 123px !important;
		height: 123px !important;
		left: calc(50% - 63px) !important;
		top: 106px !important;
	}

	.destacado>.top>.username {
		bottom: -3px !important;
	}
}

@media (max-width: 670px) {
	.destacado>.top>img.top_destacado {
		width: 121px !important;
		height: 121px !important;
		left: calc(50% - 62px) !important;
		top: 106px !important;
	}

	.destacado>.top>.username {
		bottom: 0 !important;
		font-size: 16px !important;
	}
}

@media (max-width: 659px) {
	.destacado>.top>.username {
		bottom: 4px !important;
	}

	.clasificados_destacados {
		padding-left: 20px !important;
		padding-right: 20px !important;
	}

	.clasificados_destacados>.borde_tabla {
		width: 100% !important;
	}
}

@media (max-width: 640px) {
	.destacado>.top>img.top_destacado {
		width: 121px !important;
		height: 121px !important;
		left: calc(50% - 62px) !important;
		top: 105px !important;
	}

	.destacado>.top>.username {
		bottom: 7px !important;
	}
}

@media (max-width: 630px) {
	.destacado>.top>img.top_destacado {
		width: 119px !important;
		height: 119px !important;
		left: calc(50% - 61px) !important;
		top: 106px !important;
	}

	.destacado>.top>.username {
		bottom: 7px !important;
	}

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 195px !important;
		height: 40px !important;
	}

	.destacado>.categoria {
		left: calc(50% + 95px) !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 290px) !important;
	}
}

@media (max-width: 620px) {
	.destacado>.top>img.top_destacado {
		width: 120px !important;
		height: 120px !important;
		left: calc(50% - 61px) !important;
		top: 105px !important;
	}

	.destacado>.top>.username {
		bottom: 9px !important;
	}

	.clasificados_destacados>.borde_tabla {
		height: 2100px !important;
	}
}

@media (max-width: 610px) {
	.destacado>.top>img.top_destacado {
		width: 119px !important;
		height: 119px !important;
		left: calc(50% - 61px) !important;
		top: 105px !important;
	}

	.destacado>.top>.username {
		bottom: 14px !important;
		font-size: 14px !important;
		left: calc(50% - 98px) !important;
	}

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 180px !important;
		height: 35px !important;
	}

	.destacado>.categoria {
		left: calc(50% + 85px) !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 275px) !important;
	}
}

@media (max-width: 595px) {
	.destacado>.top>img.top_destacado {
		width: 117px !important;
		height: 117px !important;
		left: calc(50% - 59px) !important;
		top: 105px !important;
	}

	.destacado>.top>.username {
		bottom: 17px !important;
	}
}

@media (max-width: 580px) {
	.destacado>.top>img.top_destacado {
		width: 115px !important;
		height: 115px !important;
		left: calc(50% - 59px) !important;
		top: 105px !important;
	}

	.destacado>.top>.username {
		bottom: 19px !important;
	}
}

@media (max-width: 572px) {

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 160px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 246px) !important;
	}

	.destacado>.categoria {
		left: calc(50% + 85px) !important;
	}

	.destacado>.top>img.top_destacado {
		width: 112px !important;
		height: 112px !important;
		left: calc(50% - 57px) !important;
		top: 107px !important;
	}

	.destacado>.top>.username {
		bottom: 20px !important;
	}
}

@media (max-width: 560px) {
	.destacado>.top>img.top_destacado {
		width: 109px !important;
		height: 109px !important;
		left: calc(50% - 55px) !important;
		top: 107px !important;
	}

	.destacado>.top>.username {
		bottom: 23px !important;
	}
}

@media (max-width: 540px) {
	.destacado>.top>img.top_destacado {
		width: 107px !important;
		height: 107px !important;
		left: calc(50% - 55px) !important;
		top: 107px !important;
	}

	.destacado>.top>.username {
		bottom: 27px !important;
	}

	.destacado>video {
		min-height: 840px !important;
	}
}

@media (max-width: 520px) {
	.destacado>.top>img.top_destacado {
		width: 105px !important;
		height: 105px !important;
		left: calc(50% - 53px) !important;
		top: 107px !important;
	}

	.destacado>.top>.username {
		bottom: 30px !important;
	}
}

@media (max-width: 500px) {
	.destacado>.top>img.top_destacado {
		width: 103px !important;
		height: 103px !important;
		left: calc(50% - 52px) !important;
		top: 107px !important;
	}

	.destacado>.top>.username {
		bottom: 33px !important;
	}

	.destacado>.categoria {
		left: calc(50% + 68px) !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 228px) !important;
	}
}

@media (max-width: 492px) {
	.destacado>.top>img.top_destacado {
		width: 99px !important;
		height: 99px !important;
		left: calc(50% - 50px) !important;
		top: 109px !important;
	}

	.destacado>.top>.username {
		bottom: 36px !important;
	}
}

@media (max-width: 480px) {

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 150px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 214px) !important;
	}

	.destacado>.categoria {
		left: calc(50% + 70px) !important;
	}

	.destacado>.top>img.top_destacado {
		width: 96px !important;
		height: 96px !important;
		left: calc(50% - 49px) !important;
		top: 110px !important;
	}

	.destacado>.top>.username {
		bottom: 37px !important;
	}
}

@media (max-width: 471px) {
	.destacado>.top>img.top_destacado {
		width: 95px !important;
		height: 95px !important;
		left: calc(50% - 49px) !important;
		top: 110px !important;
	}

	.destacado>.top>.username {
		bottom: 39px !important;
	}
}

@media (max-width: 463px) {
	.destacado>.top>img.top_destacado {
		width: 93px !important;
		height: 93px !important;
		left: calc(50% - 48px) !important;
		top: 110px !important;
	}

	.destacado>.top>.username {
		bottom: 41px !important;
	}
}

@media (max-width: 454px) {
	.destacado>.top>img.top_destacado {
		width: 91px !important;
		height: 91px !important;
		left: calc(50% - 46px) !important;
		top: 111px !important;
	}

	.destacado>.top>.username {
		bottom: 43px !important;
	}
}

@media (max-width: 440px) {

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 120px !important;
		height: 35px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 208px) !important;
	}

	.destacado>.categoria {
		left: calc(50% + 60px) !important;
	}

	.destacado>.top>img.top_destacado {
		width: 86px !important;
		height: 86px !important;
		left: calc(50% - 43px) !important;
		top: 113px !important;
	}

	.destacado>.top>.username {
		bottom: 45px !important;
	}
}

@media (max-width: 432px) {
	.destacado>.top>.foto>img.aura_foto {
		width: 336px !important;
		height: 250px !important;
		top: calc(50% - 131px) !important;
		left: calc(50% - 167px) !important;
	}

	.destacado>.top>.foto>img.marco_foto {
		width: 380px !important;
		height: 300px !important;
	}

	.descripcion_destacado {
		bottom: 39px !important;
		padding: 6px 7px 4px 9px !important;
		width: 90px !important;
	}

	.destacado>.top>.foto>img.top_destacado {
		top: calc(50% - 70px) !important;
		width: 130px !important;
		height: 130px !important;
	}
}

@media (max-width: 425px) {

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 130px !important;
		height: 35px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 198px) !important;
		font-size: 14px !important;
	}

	.destacado>.categoria {
		left: calc(50% + 45px) !important;
	}

	.destacado>.top>img.top_destacado {
		width: 84px !important;
		height: 84px !important;
		left: calc(50% - 43px) !important;
		top: 113px !important;
	}

	.destacado>.top>.username {
		bottom: 48px !important;
	}
}

@media (max-width: 415px) {

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 120px !important;
		height: 29px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 178px) !important;
	}

	.destacado>.diamantes>div>p {
		font-size: 14px !important;
	}

	.destacado>.categoria>h2 {
		font-size: 17px !important;
	}

	.destacado>.categoria {
		left: calc(50% + 65px) !important;
	}

	.destacado>.top>img.top_destacado {
		width: 82px !important;
		height: 82px !important;
		left: calc(50% - 42px) !important;
		top: 114px !important;
	}

	.destacado>.top>.username {
		bottom: 50px !important;
	}
}

@media (max-width: 400px) {
	.destacado>.top>img.top_destacado {
		width: 80px !important;
		height: 80px !important;
		left: calc(50% - 41px) !important;
		top: 114px !important;
	}

	.destacado>.top>.username {
		bottom: 52px !important;
	}

	.destacado>.top>.info {
		min-width: 90% !important;
	}
}

@media (max-width: 388px) {
	.destacado>.top>img.top_destacado {
		width: 78px !important;
		height: 78px !important;
		left: calc(50% - 39px) !important;
		top: 114px !important;
	}

	.destacado>.top>.username {
		bottom: 55px !important;
	}

	.avatar-tabla {
		width: 38px !important;
		height: 38px !important;
	}

	.destacado>.top>.foto>img.aura_foto {
		width: 325px !important;
		height: 250px !important;
		top: calc(50% - 128px) !important;
		left: calc(50% - 162px) !important;
	}

	.destacado>.top>.foto>img.marco_foto {
		width: 300px !important;
		height: 300px !important;
	}

	.descripcion_destacado {
		bottom: 39px !important;
		padding: 6px 7px 4px 9px !important;
		width: 90px !important;
	}

	.destacado>.top>.foto>img.top_destacado {
		top: calc(50% - 66px) !important;
		left: calc(50% - 60px) !important;
		width: 120px !important;
		height: 120px !important;
	}
}

@media (max-width: 378px) {
	.destacado>.top>img.top_destacado {
		width: 76px !important;
		height: 76px !important;
		left: calc(50% - 39px) !important;
		top: 114px !important;
	}

	.destacado>.top>.username {
		bottom: 57px !important;
	}

	.destacado>.diamantes>.title,
	.destacado>.categoria>div {
		width: 115px !important;
	}

	.destacado>.diamantes {
		left: calc(50% - 170px) !important;
	}

	.destacado>.categoria {
		left: calc(50% + 52px) !important;
	}

	.destacado>.top>.info>.personal {
		width: 100% !important;
	}
}

@media (max-width: 350px) {
	.destacado>.top>.foto>img.aura_foto {
		left: calc(50% - 162px) !important;
	}
}

@media (max-width: 325px) {
	.destacado>.top>.foto>img.aura_foto {
		width: 285px !important;
		height: 210px !important;
		top: calc(50% - 108px) !important;
		left: calc(50% - 142.5px) !important;
	}

	.destacado>.top>.foto>img.marco_foto {
		width: 260px !important;
		height: 260px !important;
	}

	.destacado>.top>.foto>img.top_destacado {
		top: calc(50% - 57px) !important;
		left: calc(50% - 53px) !important;
		width: 105px !important;
		height: 105px !important;
	}

	.descripcion_destacado {
		font-size: 12px !important;
		width: 60px !important;
		left: calc(50% - 30px) !important;
		bottom: 29px !important;
	}

	.link_whatsapp {
		width: 90% !important;
		height: 80px !important;
	}

	.link_whatsapp>span {
		font-size: 1.5rem !important;
		padding: 21px 15px 13px 71px !important;
	}

	.link_ver_novedades {
		align-items: center;
	}

	.link_ver_novedades>.img_btn_ver_todo {
		width: 95% !important;
	}
}
</style>