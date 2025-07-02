<template>
	<section class="resenas flex flex-column relative pb-5">
		<video src="/assets/video/home/fondo_resenas.mp4" class="absolute w-full" autoplay loop>
			<source src="/assets/video/home/fondo_resenas.mp4" type="video/mp4" />
		</video>
		<h1 class="font-jockey-one text-6xl my-3 text-center uppercase word-break w-full">RESEÑAS</h1>
		<Carousel :value="resenas" :circular="true" :showNavigators="false" :showIndicators="false"
			:autoplayInterval="2000" class="w-full resenas_usuarios carousel-items-centrados"
			:numVisible="numItemsVisible" :responsiveOptions="responsiveOptions">
			<template #item="props">
				<div class="item_resena_usuario relative flex flex-column mt-8 mb-4">
					<ScrollPanel :unstyled="true" class="descripcion"
						style="width: 100%; height: 150px; overflow: auto !important">
						<p class="m-0 text-black-alpha-90 text-start font-bold font-inter text-lg uppercase">{{
							props.data.descripcion }}</p>
					</ScrollPanel>
					<div class="flex w-full gap-1">
						<div class="foto_container">
							<img :src="props.data.foto" alt="Foto Usuario" class="border-circle" />
						</div>
						<div class="div flex flex-column gap-1">
							<h3 class="font-inter text-start uppercase m-0 text-black-alpha-90">{{ props.data.nombre }}
							</h3>
							<span class="font-inter font-bold text-black-alpha-90">{{ props.data.fecha }}</span>
						</div>
					</div>
				</div>
			</template>
		</Carousel>
	</section>
</template>
<script>
export default {
	data: () => ({
		numItemsVisible: 1,
		resenas: [
			{
				nombre: "Juan",
				foto: "/assets/img/perfil1.jpg",
				descripcion: "Lorem ipsum dolor",
				fecha: "2025-02-12",
			},
			{
				nombre: "Luis",
				foto: "/assets/img/perfil2.jpg",
				descripcion: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed euismod, ipsum id malesuada sagittis, mauris velit",
				fecha: "2025-04-22",
			},
			{
				nombre: "Pedro",
				foto: "/assets/img/perfil3.jpg",
				descripcion: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed euismod, ipsum id malesuada sagittis, mauris velit",
				fecha: "2025-03-15",
			},
			{
				nombre: "Maria",
				foto: "/assets/img/perfil1.jpg",
				descripcion: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed euismod, ipsum id malesuada sagittis, mauris velit",
				fecha: "2025-02-28",
			},
		],
		responsiveOptions: [
			{
				breakpoint: "3000px",
				numVisible: 3,
				numScroll: 1,
			},
			{
				breakpoint: "1200px",
				numVisible: 2,
				numScroll: 1,
			},
			{
				breakpoint: "800px",
				numVisible: 1,
				numScroll: 1,
			},
		],
	}),
};
</script>
<style scoped>
.resenas>video,
.resenas {
	object-fit: fill;
	height: 600px;
}

img.estrella {
	width: 34px;
	height: 34px;
}

.foto_container {
	width: 60px;
	height: 60px;
	border-radius: 50%;
}

.foto_container>img {
	width: 100%;
	height: 100%;
}

.item_resena_usuario {
	max-width: 360px;
	min-width: 350px;
	border-radius: 12px;
	padding: 15px 6px 28px 6px;
	z-index: 1;
	background: #ffffff5e;
	box-shadow: 7px 7px 9.3px 0px #00000040;
	backdrop-filter: blur(4px);
}

.item_resena_usuario>h3 {
	margin-top: 70px !important;
}

@media (max-width: 450px) {
	.item_resena_usuario {
		max-width: 300px !important;
		min-width: 300px !important;
	}
}

@media (max-width: 400px) {
	.item_resena_usuario {
		min-width: 220px !important;
		max-width: 220px !important;
	}
}

@media (max-width: 335px) {
	.item_resena_usuario {
		max-width: 210px !important;
		min-width: 210px !important;
	}
}

@media (max-width: 310px) {
	img.estrella {
		width: 24px !important;
		height: 24px !important;
	}

	.item_resena_usuario {
		max-width: 190px !important;
		min-width: 190px !important;
	}
}

@media (max-width: 235px) {
	img.estrella {
		width: 20px !important;
		height: 20px !important;
	}
}

@media (max-width: 200px) {
	img.estrella {
		width: 16px !important;
		height: 16px !important;
	}
}
</style>
<style>
.resenas>.resenas_usuarios>.p-carousel-content>ul.p-carousel-indicators>li.p-carousel-indicator>button {
	width: 18px;
	height: 18px;
	border-radius: 50%;
}

.resenas>.resenas_usuarios>.p-carousel-content>ul.p-carousel-indicators>li.p-carousel-indicator.p-highlight>button {
	background-color: #25e007;
}

.resenas_usuarios .p-carousel-items-container {
	gap: 10px !important;
}
</style>