<template>
	<div class="home">
		<NavBar />
		<div class="inicio">
			<div class="fondo">
				<div class="destacado" id="destacado">
					<video src="/assets/video/home/fondo_leones.webm" autoplay loop muted>
						<source src="/assets/video/home/fondo_leones.webm" type="video/webm" />
						Tu navegador no soporta esta funcionalidad video
					</video>
					<div class="diamantes w-max">
						<div class="title transition-all transition-duration-1000 fadein animation-duration-1000">
							<div class="animacion" />
						</div>
						<div class="flex w-full flex-wrap gap-1 justify-content-center align-items-center">
							<img
								src="/assets/img/home/diamante.gif"
								alt="Diamantes"
								class="transition-all transition-duration-1000 fadein animation-duration-1000"
								style="width: 40px; object-fit: fill"
							/>
							<p class="m-0 text-2xl text-center font-bold transition-all transition-duration-1000 fadein animation-duration-1000">
								{{ topDestacado.diamantes_mes_actual.toLocaleString() }}
							</p>
						</div>
					</div>
					<div class="top">
						<img class="fondo" src="/assets/img/home/marco-foto.png" alt="Marco foto" />
						<strong class="absolute top-0 pt-2 text-lg descripcion_destacado">{{ descripcion_destacado }}</strong>
						<img
							:src="topDestacado.foto"
							alt="Top 1"
							class="top_destacado transition-all transition-duration-1000 fadein animation-duration-1000"
						/>
						<p class="m-0 username transition-all transition-duration-1000 fadein animation-duration-1000">{{ topDestacado.usuario }}</p>
					</div>
					<div class="categoria w-max flex flex-column flex-wrap gap-1 justify-content-center align-items-center">
						<h2
							class="m-0 white-space-nowrap overflow-hidden text-overflow-ellipsis w-full text-center transition-all transition-duration-1000 fadein animation-duration-1000"
						>
							CATEGORIA
						</h2>
						<div class="rookie transition-all transition-duration-1000 fadein" v-if="topDestacado.categoria == 'Rookie'">
							<div class="animacion" />
						</div>
						<div class="veteran transition-all transition-duration-1000 fadein" v-else-if="topDestacado.categoria == 'Veteran'">
							<div class="animacion" />
						</div>
						<div class="pro transition-all transition-duration-1000 fadein" v-else-if="topDestacado.categoria == 'Pro'">
							<div class="animacion" />
						</div>
						<div class="proplus transition-all transition-duration-1000 fadein" v-else-if="topDestacado.categoria == 'Pro+'">
							<div class="animacion" />
						</div>
					</div>
				</div>
				<TopsCarouselVideos />
				<section id="unete" class="text-center flex flex-column align-items-center py-8">
					<h1 class="text-6xl mb-0 font-play-pretend-home">¡VEN Y SÉ PARTE!</h1>
					<p class="font-bold mt-0">Somos una agencia dedicada a crecer tu perfil y en ti mismo</p>
					<a
						href="https://api.whatsapp.com/send?phone=573176205370"
						target="_blank"
						class="link_whatsapp relative transition-all fadein animation-duration-1000 uppercase no-underline text-white-alpha-90"
					>
						<img src="/assets/img/btn_escribenos.png" class="img_btn_escribenos" alt="Botón WhatsApp" />
						<span class="absolute text-4xl font-play-pretend-home">ESCRÍBENOS!</span>
					</a>
				</section>
				<CarouselNovedades />
				<Phone />
				<section id="clasificados" class="clasificados_destacados p-7 flex flex-column align-items-center">
					<Panel :unstyled="true" class="borde_tabla">
						<template #header>
							<div class="containerC" style="margin-bottom: 20px" v-if="clasificados.length > 2">
								<Clasificacion :nombre="clasificados[1].usuario" top="2" tipo="Platino" :foto="clasificados[1].foto" />
								<Clasificacion top="1" tipo="Oro" :nombre="clasificados[0].usuario" :foto="clasificados[0].foto" />
								<Clasificacion :nombre="clasificados[2].usuario" top="3" tipo="Cobre" :foto="clasificados[2].foto" />
							</div>
						</template>
						<DataTable
							:unstyled="true"
							scrollable
							:value="clasificados"
							class="mt-7 tabla_destacados_home color-blue font-bold"
							:tableStyle="{ 'min-width': '100%', 'text-align': 'start' }"
						>
							<Column header="#" style="min-width: 20px" frozen headerClass="text-center color-blue">
								<template #body="props">
									<div class="w-full flex justify-content-center">
										<Clasificacion
											v-if="props.index == 1"
											:nombre="clasificados[1].usuario"
											top="2"
											tipo="PlatinoPequeno"
											:foto="clasificados[1].foto"
											:mostrarNombre="false"
											class="clasificacion_fila_tabla"
										/>
										<Clasificacion
											v-else-if="props.index == 0"
											top="1"
											tipo="OroPequeno"
											:nombre="clasificados[0].usuario"
											:foto="clasificados[0].foto"
											:mostrarNombre="false"
											class="clasificacion_fila_tabla"
										/>
										<Clasificacion
											v-else-if="props.index == 2"
											:nombre="clasificados[2].usuario"
											top="3"
											tipo="CobrePequeno"
											:foto="clasificados[2].foto"
											:mostrarNombre="false"
											class="clasificacion_fila_tabla"
										/>
										<strong v-else>{{ props.index + 1 }}</strong>
									</div>
								</template>
							</Column>
							<Column field="usuario" header="Creador" headerClass="text-left" />
							<Column header="Insignias Obtenidas ⭐" headerClass="text-left">
								<template #body="slotProps">
									<div class="misInsignias flex w-full gap-1 flex-nowrap justify-content-start">
										<Avatar
											v-for="(insignia, index) in slotProps.data.insignias"
											:key="index"
											size="large"
											shape="circle"
											v-tooltip="insignia.descripcion"
										>
											<img :src="insignia.secure_url" :alt="`Insignia ${index + 1}`" />
										</Avatar>
									</div>
								</template>
							</Column>
							<Column field="grupo" header="Grupo" headerClass="text-left">
								<template #body="props">
									<img :src="`/assets/img/grupos/${props.data.grupo}.png`" :alt="`Grupo ${props.data.grupo}`" class="img-grupo" />
								</template>
							</Column>
						</DataTable>
					</Panel>
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
			},
			{
				usuario: "x",
				foto: "",
			},
			{
				usuario: "x",
				foto: "",
			},
		],
		top5Diamantes: [],
		topDiamantesCategorias: [],
		indexTopDestacado: 0,
		indexTopCategoria: 0,
		topDestacadoTitle: "Diamantes",
		idIntervalDestacado: null,
		topDestacado: {
			categoria: null,
			diamantes_mes_actual: 0,
			foto: "",
			usuario: "",
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
	background: #000000;
	box-sizing: border-box;
	scroll-behavior: smooth !important;
}

.home {
	background: #000000;
}

.destacado {
	width: 100%;
	height: max-content;
	max-height: 650px;
}
.destacado > * {
	width: 100%;
	height: 100%;
	object-fit: contain;
	object-position: top;
}
.destacado > .diamantes > .title {
	background-image: url("/assets/img/home/diamantes-title.png");
	background-repeat: no-repeat;
	background-position: center;
	background-size: 100% 100%;
	object-fit: contain;
	height: 54px;
	width: 340px;
	margin: 0;
}
.destacado > .diamantes > .title > .animacion,
.destacado > .categoria > div > .animacion {
	height: 100%;
	width: 100%;
	background: url("/assets/img/home/electricidad.gif");
	background-size: 100% 100%;
	object-fit: contain;
	mix-blend-mode: lighten;
	background-repeat: no-repeat;
}
.destacado > .diamantes {
	position: absolute;
	left: calc(50% - 507px);
	top: 222px;
	height: auto;
}
.destacado > .categoria {
	position: absolute;
	text-align: center;
	left: calc(50% + 153px);
	top: 208px;
	height: auto;
}
.descripcion_destacado {
	text-shadow: 2px 2px 9px white;
}
.destacado > .categoria > div {
	pointer-events: none;
	background-repeat: no-repeat;
	background-position: top;
	background-size: 100% 100%;
	object-fit: contain;
	height: 54px;
	width: 340px;
	margin: 0;
}
.destacado > .categoria > .rookie {
	background-image: url("/assets/img/grupos/rookie.png");
}
.destacado > .categoria > .veteran {
	background-image: url("/assets/img/grupos/veterano.png");
}
.destacado > .categoria > .pro {
	background-image: url("/assets/img/grupos/pro.png");
}
.destacado > .categoria > .proplus {
	background-image: url("/assets/img/grupos/pro+.png");
}
.destacado > video {
	min-height: 540px;
	height: auto;
	object-fit: cover;
	max-height: 650px;
}
.destacado > .top {
	position: absolute;
	display: flex;
	justify-content: center;
	align-items: center;
	top: 137px;
}
.destacado > .top > img.fondo {
	width: 80%;
	max-width: 1041px;
	object-fit: contain;
	background-size: contain;
	background-repeat: no-repeat;
}
.destacado > .top > img.top_destacado {
	position: absolute;
	border-radius: 50%;
	top: 95px;
	left: calc(50% - 92px);
	width: 181px;
	height: 181px;
}
.destacado > .top > .username {
	position: absolute;
	text-align: center;
	width: 208px;
	font-weight: bold;
	font-size: 24px;
	max-width: 208px;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
	bottom: -78px;
	left: calc(50% - 94px);
}
.destacado > .categoria > h2 {
	line-height: 0.85;
}
.link_whatsapp {
	width: 325px;
	height: 78px;
	display: flex;
	flex-direction: column;
}
.link_whatsapp > .img_btn_escribenos {
	height: 100%;
	background-size: 100% 100%;
}
.link_whatsapp > span {
	padding: 15px 11px 13px 71px;
	text-align: start;
	width: 100%;
}

.clasificados_destacados {
	background-image: url("/assets/img/home/fondo_tabla_destacados.png");
	background-repeat: no-repeat;
	background-size: 100% 100%;
}
.clasificados_destacados > .borde_tabla {
	background-image: url("/assets/img/home/borde_tabla_destacados.png");
	background-repeat: no-repeat;
	background-size: 100% 100%;
	padding: 40px;
	height: 1200px;
	width: 1200px;
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

.row > * {
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
.clasificados_destacados > .borde_tabla > div:last-child > div > div > div {
	max-height: 578px;
	height: 100%;
}
.clasificados_destacados > .borde_tabla > div:last-child {
	height: 50%;
}
.clasificados_destacados > .borde_tabla > div:last-child > *,
.tabla_destacados_home {
	height: 100%;
}
.clasificados_destacados > .borde_tabla > div:last-child > div > .tabla_destacados_home > div:first-child > table > thead > tr > th {
	border-spacing: 0;
}
.clasificados_destacados > .borde_tabla > div:last-child > div > .tabla_destacados_home > div:first-child > table > thead > tr {
	background-image: url("/assets/img/eventos/divisor-fila.png") !important;
	background-position: bottom;
	border-spacing: 0 !important;
	background-repeat: repeat-x !important;
	background-size: contain !important;
}
@media (max-width: 1263px) {
	.destacado > .top > img.top_destacado {
		width: 178px !important;
		height: 178px !important;
		left: calc(50% - 90px) !important;
	}
	.destacado > .top > .username {
		bottom: -72px !important;
	}
}
@media (max-width: 1254px) {
	.clasificados_destacados > .borde_tabla {
		height: 1300px !important;
	}
}
@media (max-width: 1240px) {
	.destacado > .top > img.top_destacado {
		width: 176px !important;
		height: 176px !important;
		left: calc(50% - 89px) !important;
	}

	.destacado > .top > .username {
		bottom: -68px !important;
	}
	.descripcion_destacado {
		top: 11px !important;
	}
}

@media (max-width: 1213px) {
	.destacado > .top > .username {
		bottom: -64px !important;
	}
}
@media (max-width: 1200px) {
	.clasificados_destacados > .borde_tabla {
		width: 1000px !important;
		height: 1650px !important;
	}
}
@media (max-width: 1185px) {
	.destacado > .top > img.top_destacado {
		width: 167px !important;
		height: 167px !important;
		left: calc(50% - 85px) !important;
		top: 98px !important;
	}
	.destacado > .top > .username {
		bottom: -59px !important;
	}
}
@media (max-width: 1170px) {
	.destacado > .top > .username {
		bottom: -53px !important;
	}
	.descripcion_destacado {
		top: 16px !important;
	}
}
@media (max-width: 1125px) {
	.destacado > .top > img.top_destacado {
		width: 158px !important;
		height: 158px !important;
		left: calc(50% - 79px) !important;
		top: 100px !important;
	}

	.destacado > .top > .username {
		bottom: -51px !important;
		font-size: 22px !important;
	}
}
@media (max-width: 1111px) {
	.destacado > .top > img.fondo {
		width: 90% !important;
	}
	.destacado > .top > img.top_destacado {
		width: 170px !important;
		height: 170px !important;
		left: calc(50% - 86px) !important;
		top: 99px !important;
	}

	.destacado > .top > .username {
		bottom: -70px !important;
	}
	.descripcion_destacado {
		top: 11px !important;
	}
}
@media (max-width: 1093px) {
	.destacado > .top > img.top_destacado {
		left: calc(50% - 86px) !important;
		top: 98px !important;
	}

	.destacado > .top > .username {
		bottom: -66px !important;
	}
	.destacado > .categoria > div,
	.destacado > .diamantes > .title {
		width: 320px !important;
	}
}
@media (max-width: 1077px) {
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 300px;
	}
	.destacado > .top > .username {
		bottom: -62px !important;
	}
}
@media (max-width: 1051px) {
	.destacado > .top > img.top_destacado {
		width: 166px !important;
		height: 166px !important;
		left: calc(50% - 84px) !important;
		top: 98px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 460px) !important;
	}
	.destacado > .top > .username {
		bottom: -57px !important;
	}
}
@media (max-width: 1024px) {
	.destacado > .top > img.top_destacado {
		width: 162px !important;
		height: 162px !important;
		left: calc(50% - 82px) !important;
		top: 99px !important;
	}
	.destacado > .top > .username {
		bottom: -53px !important;
	}
	.descripcion_destacado {
		top: 16px !important;
	}
}
@media (max-width: 1000px) {
	.clasificados_destacados > .borde_tabla {
		width: 800px !important;
		height: 1650px !important;
	}
}
@media (max-width: 998px) {
	.destacado > .top > img.top_destacado {
		width: 158px !important;
		height: 158px !important;
		left: calc(50% - 80px) !important;
		top: 100px !important;
	}
	.destacado > .top > .username {
		bottom: -49px !important;
	}
}
@media (max-width: 984px) {
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 280px !important;
	}
	.destacado > .top > img.top_destacado {
		width: 156px !important;
		height: 156px !important;
		left: calc(50% - 78px) !important;
		top: 100px !important;
	}
	.destacado > .top > .username {
		bottom: -47px !important;
	}
	.descripcion_destacado {
		top: 19px !important;
	}
}
@media (max-width: 970px) {
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 250px !important;
	}
	.destacado > .top > .username {
		bottom: -44px !important;
	}
}
@media (max-width: 948px) {
	.destacado > .top > img.top_destacado {
		width: 149px !important;
		height: 149px !important;
		left: calc(50% - 76px) !important;
		top: 102px !important;
	}
	.destacado > .top > .username {
		bottom: -40px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 415px) !important;
	}
	.destacado > .diamantes,
	.destacado > .categoria {
		top: 250px !important;
	}
	.descripcion_destacado {
		top: 24px !important;
	}
}
@media (max-width: 929px) {
	.destacado > video {
		object-fit: fill !important;
	}
	.destacado > .top > img.top_destacado {
		width: 149px !important;
		height: 149px !important;
		left: calc(50% - 76px) !important;
		top: 102px !important;
	}
	.destacado > .top > .username {
		bottom: -36px !important;
		font-size: 20px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 398px) !important;
	}
	.destacado > .diamantes,
	.destacado > .categoria {
		top: 260px !important;
	}
}
@media (max-width: 900px) {
	.destacado > .top > img.fondo {
		width: 98% !important;
	}
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 250px !important;
	}
	.destacado > .top > .username {
		bottom: -44px !important;
	}
	.destacado > .top > img.top_destacado {
		width: 153px !important;
		height: 153px !important;
		left: calc(50% - 77px) !important;
		top: 102px !important;
	}
	.descripcion_destacado {
		top: 18px !important;
	}
}
@media (max-width: 878px) {
	.destacado > .top > img.top_destacado {
		left: calc(50% - 75px) !important;
		width: 150px !important;
		height: 150px !important;
	}

	.destacado > .top > .username {
		bottom: -41px !important;
	}
	.destacado > .categoria {
		right: 9%;
	}
	.descripcion_destacado {
		top: 23px !important;
	}
}
@media (max-width: 860px) {
	.destacado > .top > img.top_destacado {
		top: 103px !important;
		left: calc(50% - 73px) !important;
		width: 145px !important;
		height: 145px !important;
	}

	.destacado > .top > .username {
		bottom: -35px !important;
	}
	.destacado > .categoria {
		left: calc(50% + 124px) !important;
	}
}
@media (max-width: 825px) {
	.destacado > .top > img.top_destacado {
		top: 104px !important;
		left: calc(50% - 71px) !important;
		width: 140px !important;
		height: 140px !important;
	}

	.destacado > .top > .username {
		bottom: -31px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 382px) !important;
	}
	.destacado > .categoria {
		left: calc(50% + 118px) !important;
	}
	.descripcion_destacado {
		top: 30px !important;
	}
}
@media (max-width: 809px) {
	.destacado > .top > img.top_destacado {
		top: 105px !important;
		left: calc(50% - 70px) !important;
		width: 137px !important;
		height: 137px !important;
	}

	.destacado > .top > .username {
		bottom: -28px !important;
	}
	.clasificados_destacados > .borde_tabla {
		width: 650px !important;
		height: 2000px !important;
	}
}
@media (max-width: 795px) {
	.destacado > .top > img.top_destacado {
		top: 106px !important;
		left: calc(50% - 68px) !important;
		width: 135px !important;
		height: 135px !important;
	}

	.destacado > .top > .username {
		bottom: -25px !important;
		font-size: 18px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 367px) !important;
	}
	.destacado > .categoria {
		left: calc(50% + 100px) !important;
	}
}
@media (max-width: 782px) {
	.destacado > .top > img.top_destacado {
		top: 106px !important;
		left: calc(50% - 67px) !important;
		width: 132px !important;
		height: 132px !important;
	}
	.destacado > .diamantes > .title > .animacion,
	.destacado > .categoria > div > .animacion {
		object-fit: fill !important;
	}
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 230px !important;
		height: 50px !important;
	}
	.destacado > .top > .username {
		bottom: -21px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 367px) !important;
	}
	.destacado > .categoria {
		left: calc(50% + 115px) !important;
	}
	.descripcion_destacado {
		top: 31px !important;
	}
}
@media (max-width: 760px) {
	.destacado > .top > .username {
		bottom: -16px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 350px) !important;
	}
	.destacado > .categoria {
		left: calc(50% + 115px) !important;
	}
}
@media (max-width: 750px) {
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 200px !important;
		height: 45px !important;
	}
	.destacado > .diamantes,
	.destacado > .categoria {
		top: 264px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 335px) !important;
	}
	.destacado > .top > img.top_destacado {
		width: 130px !important;
		height: 130px !important;
		left: calc(50% - 65px) !important;
		top: 106px !important;
	}
	.destacado > .top > .username {
		bottom: -15px !important;
	}
	.descripcion_destacado {
		top: 36px !important;
	}
}
@media (max-width: 732px) {
	.destacado > .top > img.top_destacado {
		width: 130px !important;
		height: 130px !important;
		left: calc(50% - 65px) !important;
		top: 105px !important;
	}
	.destacado > .top > .username {
		bottom: -13px !important;
	}
}
@media (max-width: 721px) {
	.destacado > .top > img.top_destacado {
		width: 128px !important;
		height: 128px !important;
		left: calc(50% - 65px) !important;
		top: 105px !important;
	}
	.destacado > .top > .username {
		bottom: -9px !important;
	}
	.descripcion_destacado {
		top: 38px !important;
	}
}
@media (max-width: 700px) {
	.destacado > .categoria {
		left: calc(50% + 105px) !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 313px) !important;
	}
	.destacado > .top > img.top_destacado {
		width: 125px !important;
		height: 125px !important;
		left: calc(50% - 63px) !important;
		top: 106px !important;
	}
	.destacado > .top > .username {
		bottom: -6px !important;
	}
}
@media (max-width: 686px) {
	.destacado > .top > img.top_destacado {
		width: 123px !important;
		height: 123px !important;
		left: calc(50% - 63px) !important;
		top: 106px !important;
	}
	.destacado > .top > .username {
		bottom: -3px !important;
	}
	.descripcion_destacado {
		font-size: 15px !important;
		top: 45px !important;
	}
}
@media (max-width: 670px) {
	.destacado > .top > img.top_destacado {
		width: 121px !important;
		height: 121px !important;
		left: calc(50% - 62px) !important;
		top: 106px !important;
	}
	.destacado > .top > .username {
		bottom: 0 !important;
		font-size: 16px !important;
	}
}
@media (max-width: 659px) {
	.destacado > .top > .username {
		bottom: 4px !important;
	}
	.clasificados_destacados {
		padding-left: 20px !important;
		padding-right: 20px !important;
	}
	.clasificados_destacados > .borde_tabla {
		width: 100% !important;
	}
	.descripcion_destacado {
		top: 49px !important;
	}
}
@media (max-width: 640px) {
	.destacado > .top > img.top_destacado {
		width: 121px !important;
		height: 121px !important;
		left: calc(50% - 62px) !important;
		top: 105px !important;
	}
	.destacado > .top > .username {
		bottom: 7px !important;
	}
}
@media (max-width: 630px) {
	.destacado > .top > img.top_destacado {
		width: 119px !important;
		height: 119px !important;
		left: calc(50% - 61px) !important;
		top: 106px !important;
	}
	.destacado > .top > .username {
		bottom: 7px !important;
	}
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 195px !important;
		height: 40px !important;
	}
	.destacado > .categoria {
		left: calc(50% + 95px) !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 290px) !important;
	}
}
@media (max-width: 620px) {
	.destacado > .top > img.top_destacado {
		width: 120px !important;
		height: 120px !important;
		left: calc(50% - 61px) !important;
		top: 105px !important;
	}
	.destacado > .top > .username {
		bottom: 9px !important;
	}
	.clasificados_destacados > .borde_tabla {
		height: 2100px !important;
	}
}
@media (max-width: 610px) {
	.destacado > .top > img.top_destacado {
		width: 119px !important;
		height: 119px !important;
		left: calc(50% - 61px) !important;
		top: 105px !important;
	}
	.destacado > .top > .username {
		bottom: 14px !important;
		font-size: 14px !important;
		left: calc(50% - 98px) !important;
	}
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 180px !important;
		height: 35px !important;
	}
	.destacado > .categoria {
		left: calc(50% + 85px) !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 275px) !important;
	}
	.descripcion_destacado {
		top: 54px !important;
	}
}
@media (max-width: 595px) {
	.destacado > .top > img.top_destacado {
		width: 117px !important;
		height: 117px !important;
		left: calc(50% - 59px) !important;
		top: 105px !important;
	}
	.destacado > .top > .username {
		bottom: 17px !important;
	}
}
@media (max-width: 580px) {
	.destacado > .top > img.top_destacado {
		width: 115px !important;
		height: 115px !important;
		left: calc(50% - 59px) !important;
		top: 105px !important;
	}
	.destacado > .top > .username {
		bottom: 19px !important;
	}
}
@media (max-width: 572px) {
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 160px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 246px) !important;
	}
	.destacado > .categoria {
		left: calc(50% + 85px) !important;
	}
	.destacado > .top > img.top_destacado {
		width: 112px !important;
		height: 112px !important;
		left: calc(50% - 57px) !important;
		top: 107px !important;
	}
	.destacado > .top > .username {
		bottom: 20px !important;
	}
}
@media (max-width: 560px) {
	.destacado > .top > img.top_destacado {
		width: 109px !important;
		height: 109px !important;
		left: calc(50% - 55px) !important;
		top: 107px !important;
	}
	.destacado > .top > .username {
		bottom: 23px !important;
	}
	.descripcion_destacado {
		top: 58px !important;
	}
}
@media (max-width: 540px) {
	.destacado > .top > img.top_destacado {
		width: 107px !important;
		height: 107px !important;
		left: calc(50% - 55px) !important;
		top: 107px !important;
	}
	.destacado > .top > .username {
		bottom: 27px !important;
	}
}
@media (max-width: 520px) {
	.destacado > .top > img.top_destacado {
		width: 105px !important;
		height: 105px !important;
		left: calc(50% - 53px) !important;
		top: 107px !important;
	}
	.destacado > .top > .username {
		bottom: 30px !important;
	}
	.descripcion_destacado {
		top: 63px !important;
	}
}
@media (max-width: 500px) {
	.destacado > .top > img.top_destacado {
		width: 103px !important;
		height: 103px !important;
		left: calc(50% - 52px) !important;
		top: 107px !important;
	}
	.destacado > .top > .username {
		bottom: 33px !important;
	}
	.destacado > .categoria {
		left: calc(50% + 68px) !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 228px) !important;
	}
}
@media (max-width: 492px) {
	.destacado > .top > img.top_destacado {
		width: 99px !important;
		height: 99px !important;
		left: calc(50% - 50px) !important;
		top: 109px !important;
	}
	.destacado > .top > .username {
		bottom: 36px !important;
	}
}
@media (max-width: 480px) {
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 150px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 214px) !important;
	}
	.destacado > .categoria {
		left: calc(50% + 70px) !important;
	}
	.destacado > .top > img.top_destacado {
		width: 96px !important;
		height: 96px !important;
		left: calc(50% - 49px) !important;
		top: 110px !important;
	}
	.destacado > .top > .username {
		bottom: 37px !important;
	}
}
@media (max-width: 471px) {
	.destacado > .top > img.top_destacado {
		width: 95px !important;
		height: 95px !important;
		left: calc(50% - 49px) !important;
		top: 110px !important;
	}
	.destacado > .top > .username {
		bottom: 39px !important;
	}
}
@media (max-width: 463px) {
	.destacado > .top > img.top_destacado {
		width: 93px !important;
		height: 93px !important;
		left: calc(50% - 48px) !important;
		top: 110px !important;
	}
	.destacado > .top > .username {
		bottom: 41px !important;
	}
	.descripcion_destacado {
		top: 68px !important;
	}
}
@media (max-width: 454px) {
	.destacado > .top > img.top_destacado {
		width: 91px !important;
		height: 91px !important;
		left: calc(50% - 46px) !important;
		top: 111px !important;
	}
	.destacado > .top > .username {
		bottom: 43px !important;
	}
}
@media (max-width: 440px) {
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 120px !important;
		height: 35px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 208px) !important;
	}
	.destacado > .categoria {
		left: calc(50% + 60px) !important;
	}
	.destacado > .top > img.top_destacado {
		width: 86px !important;
		height: 86px !important;
		left: calc(50% - 43px) !important;
		top: 113px !important;
	}
	.destacado > .top > .username {
		bottom: 45px !important;
	}
}
@media (max-width: 425px) {
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 130px !important;
		height: 35px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 198px) !important;
		font-size: 14px !important;
	}
	.destacado > .categoria {
		left: calc(50% + 45px) !important;
	}
	.destacado > .top > img.top_destacado {
		width: 84px !important;
		height: 84px !important;
		left: calc(50% - 43px) !important;
		top: 113px !important;
	}
	.destacado > .top > .username {
		bottom: 48px !important;
	}
}
@media (max-width: 415px) {
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 120px !important;
		height: 29px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 178px) !important;
	}
	.destacado > .diamantes > div > p {
		font-size: 14px !important;
	}
	.destacado > .categoria > h2 {
		font-size: 17px !important;
	}
	.destacado > .categoria {
		left: calc(50% + 65px) !important;
	}
	.destacado > .top > img.top_destacado {
		width: 82px !important;
		height: 82px !important;
		left: calc(50% - 42px) !important;
		top: 114px !important;
	}
	.destacado > .top > .username {
		bottom: 50px !important;
	}
	.descripcion_destacado {
		top: 72px !important;
	}
}
@media (max-width: 400px) {
	.destacado > .top > img.top_destacado {
		width: 80px !important;
		height: 80px !important;
		left: calc(50% - 41px) !important;
		top: 114px !important;
	}
	.destacado > .top > .username {
		bottom: 52px !important;
	}
}
@media (max-width: 388px) {
	.destacado > .top > img.top_destacado {
		width: 78px !important;
		height: 78px !important;
		left: calc(50% - 39px) !important;
		top: 114px !important;
	}
	.destacado > .top > .username {
		bottom: 55px !important;
	}
	.avatar-tabla {
		width: 38px !important;
		height: 38px !important;
	}
	.descripcion_destacado {
		top: 76px !important;
	}
}
@media (max-width: 378px) {
	.destacado > .top > img.top_destacado {
		width: 76px !important;
		height: 76px !important;
		left: calc(50% - 39px) !important;
		top: 114px !important;
	}
	.destacado > .top > .username {
		bottom: 57px !important;
	}
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 115px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 170px) !important;
	}
	.destacado > .categoria {
		left: calc(50% + 52px) !important;
	}
}
@media (max-width: 350px) {
	.destacado > .top > img.top_destacado {
		width: 70px !important;
		height: 70px !important;
		left: calc(50% - 35px) !important;
		top: 116px !important;
	}
	.destacado > .top > .username {
		bottom: 61px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 160px) !important;
	}
	.destacado > .categoria {
		left: calc(50% + 45px) !important;
	}
	.descripcion_destacado {
		top: 79px !important;
	}
}
@media (max-width: 325px) {
	.destacado > .top > img.top_destacado {
		width: 68px !important;
		height: 68px !important;
		left: calc(50% - 34px) !important;
		top: 116px !important;
	}
	.destacado > .top > .username {
		bottom: 67px !important;
	}
	.destacado > .diamantes {
		left: calc(50% - 151px) !important;
	}
	.destacado > .categoria {
		left: calc(50% + 41px) !important;
	}
	.destacado > .diamantes > .title,
	.destacado > .categoria > div {
		width: 109px !important;
	}
	.link_whatsapp {
		width: 90% !important;
		height: 80px !important;
	}
	.link_whatsapp > span {
		font-size: 1.5rem !important;
		padding: 21px 15px 13px 71px !important;
	}
	.link_ver_novedades {
		align-items: center;
	}
	.link_ver_novedades > .img_btn_ver_todo {
		width: 95% !important;
	}
}
</style>