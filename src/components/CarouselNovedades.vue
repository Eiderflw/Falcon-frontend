<template>
	<section id="novedades" class="novedades relative">
		<video src="/assets/video/home/fondo_novedades.mp4" class="fondo w-full absolute" autoplay loop muted>
			<source src="/assets/video/home/fondo_novedades.mp4" type="video/mp4" />
		</video>
		<div class="containerC pb-5 flex-column align-items-center relative">
			<h1 class="mb-0 text-6xl word-break font-bahiana text-white uppercase w-full text-center">NOTICIAS MÁS RECIENTES</h1>
			<Carousel
				:value="novedades"
				:numVisible="numItemsVisible"
				:showNavigators="true"
				:showIndicators="false"
				circular
				:autoplayInterval="300000"
				class="w-12 carousel-items-centrados"
				:responsiveOptions="responsiveOptions"
				ref="refsNovedades"
			>
				<template #item="props">
					<div
						class="item_novedad flex flex-column align-items-center justify-content-start gap-1"
						@mouseenter="stopAutoplay"
						@mouseleave="startAutoplay"
						@focus="stopAutoplay"
						@blur="startAutoplay"
					>
						<h1 class="text-center m-0 p-0 w-full uppercase font-onest title">{{ props.data.titulo }}</h1>
						<div class="w-full overflow-auto mb-2 descripcion font-oswald text-lg" style="word-break: break-word">
							<p v-html="props.data.descripcion" class="font-oswald" style="font-weight: 300" />
						</div>

						<div class="flex justify-content-center w-full">
							<button class="mas-informacion uppercase border-none text-2xl cursor-pointer">SABER MÁS</button>
						</div>
					</div>
				</template>
			</Carousel>
		</div>
	</section>
</template>
<script>
import axios from "axios";
export default {
	data: () => ({
		API: import.meta.env.VITE_APP_API,
		numItemsVisible: 1,
		novedades: [],
		responsiveOptions: [
			{
				breakpoint: "3000px",
				numVisible: 3,
				numScroll: 1,
			},
			{
				breakpoint: "990px",
				numVisible: 2,
				numScroll: 1,
			},
			{
				breakpoint: "730px",
				numVisible: 1,
				numScroll: 1,
			},
		],
	}),
	methods: {
		stopAutoplay() {
			this.$refs.refsNovedades.stopAutoplay();
		},
		startAutoplay() {
			this.$refs.refsNovedades.startAutoplay();
		},
	},
	async created() {
		await axios.get(`${this.API}/regla-actualizacion/nuevas`).then((resp) => {
			this.novedades = resp.data;
		});
		if (this.novedades.length == 0) {
			this.novedades = [
				{
					titulo: "NUevo",
					descripcion:
						"Lorem ipsum dolor sit amet consectetur adipisicing elit. Perferendis ad doloribus similique voluptatibus nostrum dolor, harum praesentium non! Labore impedit placeat modi exercitationem excepturi molestias accusamus perspiciatis provident deserunt quaerat.",
					tipo: "Información",
					fecha: new Date().toISOString(),
				},
				{
					titulo: "NUevo",
					descripcion:
						"Lorem ipsum dolor sit amet consectetur adipisicing elit. Perferendis ad doloribus similique voluptatibus nostrum dolor, harum praesentium non! Labore impedit placeat modi exercitationem excepturi molestias accusamus perspiciatis provident deserunt quaerat.",
					tipo: "Información",
					fecha: new Date().toISOString(),
				},
				{
					titulo: "NUevo",
					descripcion:
						"Lorem ipsum dolor sit amet consectetur adipisicing elit. Perferendis ad doloribus similique voluptatibus nostrum dolor, harum praesentium non! Labore impedit placeat modi exercitationem excepturi molestias accusamus perspiciatis provident deserunt quaerat.",
					tipo: "Información",
					fecha: new Date().toISOString(),
				},
			];
		}
	},
};
</script>
<style scoped>
.descripcion {
	height: 250px;
	max-height: 250px;
}
.descripcion::-webkit-scrollbar {
	width: 8px;
}
.descripcion::-webkit-scrollbar-track {
	background: #555;
	border-radius: 10px;
	cursor: pointer;
}
.descripcion::-webkit-scrollbar-thumb {
	background: #264157;
	border-radius: 10px;
	cursor: pointer;
}
.descripcion::-webkit-scrollbar-thumb:hover {
	background: #1e6572b5;
}

.novedades > .fondo,
.novedades {
	height: 700px;
	object-fit: fill;
}

.mas-informacion {
	background: #cccaca;
	background: radial-gradient(circle, rgba(204, 202, 202, 1) 0%, rgba(255, 255, 255, 0.43) 100%);
	text-shadow: 0px 2px 3px rgba(92, 173, 191, 1);
	padding: 8px 16px;
	border-radius: 30px;
}
.containerC {
	z-index: 2;
}

.item_novedad {
	background: linear-gradient(180deg, #264157 0%, rgba(30, 101, 114, 0) 100%);
	box-shadow: -12px 12px 37.3px 0px #1e6572b5;
	box-shadow: -12px 12px 48.4px 0px #ffffff66;
	background-size: 100% 100%;
	background-repeat: no-repeat;
	margin: 25px 10px;
	width: 320px;
	max-width: 330px;
	padding: 20px 25px;
	height: 420px;
	border-radius: 10px;
	overflow: hidden;
}
.item_novedad > .title {
	color: white;
	box-shadow: 0px 4px 4px 0px #00000040 inset;
	font-weight: 900;
}
.item_novedad > .tipo_novedad {
	background: transparent;
	color: white;
	border-radius: 12px;
	padding: 2px 10px;
}
.item_novedad .indicador_fecha {
	background: transparent;
	color: white;
	border-radius: 12px;
	padding: 2px 10px;
}
.item_novedad > .tipo_novedad.regla {
	outline: 3px solid #9b0097;
}
.item_novedad > .tipo_novedad:not(.regla) {
	outline: 3px solid #26cc00;
}
.item_novedad .indicador_fecha.regla {
	background-color: #9b0097;
}
.item_novedad .indicador_fecha:not(.regla) {
	background-color: #26cc00;
}
.link_ver_novedades {
	width: 325px;
	height: 60px;
	display: flex;
	flex-direction: column;
}
.link_ver_novedades > .img_btn_ver_todo {
	height: 100%;
	background-size: 100% 100%;
}
.link_ver_novedades > span {
	padding: 4px 47px 0px 38px;
	text-align: start;
	width: 100%;
}

@media (max-width: 990px) {
	.item_novedad {
		width: 300px !important;
	}
}
@media (max-width: 400px) {
	.item_novedad {
		width: 99% !important;
	}
}
@media (max-width: 330px) {
	.item_novedad {
		width: 98% !important;
	}
}
</style>