<template>
	<section id="novedades" class="novedades">
		<div class="containerC pb-5 flex-column align-items-center">
			<h1 class="mb-0 text-6xl color-verde font-play-pretend-home word-break">Novedades</h1>
			<Carousel
				:value="novedades"
				:numVisible="numItemsVisible"
				:showNavigators="true"
				:showIndicators="false"
				circular
				:autoplayInterval="3000"
				class="w-12 carousel-items-centrados"
				:responsiveOptions="responsiveOptions"
				ref="refsNovedades"
			>
				<template #item="props">
					<div
						class="item_novedad flex flex-column align-items-end gap-1"
						@mouseenter="stopAutoplay"
						@mouseleave="startAutoplay"
						@focus="stopAutoplay"
						@blur="startAutoplay"
					>
						<h1 class="text-right mb-0 font-bold">{{ props.data.titulo }}</h1>
						<div :class="`tipo_novedad uppercase font-bold w-max text-xs ${props.data.tipo.toLowerCase()}`">
							<span>{{ props.data.tipo }}</span>
						</div>
						<div class="w-full overflow-auto mb-2 descripcion" style="word-break: break-word">
							<p v-html="props.data.descripcion" class="font-bold" />
						</div>

						<div class="flex justify-content-start w-full">
							<div :class="`indicador_fecha uppercase font-bold w-max text-xs  ${props.data.tipo.toLowerCase()}`">
								<span>{{ props.data.fecha.slice(0, 10) }}</span>
							</div>
						</div>
					</div>
				</template>
			</Carousel>
			<router-link
				class="link_ver_novedades relative transition-all fadein animation-duration-1000 uppercase no-underline text-white-alpha-90"
				to="/actualizaciones-reglas"
			>
				<img src="/assets/img/btn_ver_todo.png" class="img_btn_ver_todo" alt="Ver todas las novedades" />
				<span class="absolute text-5xl font-play-pretend-home">VER TODO</span>
			</router-link>
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
	background: #5e951c;
	border-radius: 10px;
	cursor: pointer;
}
.descripcion::-webkit-scrollbar-thumb:hover {
	background: #84dc09;
}
.novedades {
	background-image: url("/assets/img/home/fondo_novedades.png");
	background-repeat: no-repeat;
	background-size: 100% 100%;
}
.item_novedad {
	background-image: url("/assets/img/home/item-carousel-novedades.png");
	background-size: 100% 100%;
	background-repeat: no-repeat;
	margin: 0 10px;
	width: 320px;
	max-width: 330px;
	padding: 20px 25px;
	height: 420px;
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

@media (max-width: 330px) {
	.item_novedad {
		width: 98% !important;
	}
}
</style>