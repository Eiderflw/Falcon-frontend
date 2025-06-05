<template>
	<section class="resenas flex flex-column relative pb-5">
		<h1 class="font-play-pretend-home text-6xl my-3 text-center uppercase word-break w-full">RESEÑAS</h1>
		<Carousel
			:value="resenas"
			:circular="true"
			:showNavigators="true"
			:showIndicators="true"
			:autoplayInterval="2000"
			class="w-full resenas_usuarios carousel-items-centrados"
			:numVisible="numItemsVisible"
			:responsiveOptions="responsiveOptions"
		>
			<template #item="props">
				<div class="item_resena_usuario relative mt-8 mb-4">
					<div class="foto_container absolute">
						<img :src="props.data.foto" alt="Foto Usuario" class="border-circle" />
					</div>
					<h3 class="m-2 font-play-pretend-home text-center">{{ props.data.nombre }}</h3>
					<ScrollPanel :unstyled="true" class="descripcion" style="width: 100%; height: 150px; overflow: auto !important">
						<p class="m-0 text-white-alpha-70 text-center">{{ props.data.descripcion }}</p>
					</ScrollPanel>
					<div class="estrellas w-full flex gap-3 pt-2 mt-auto justify-content-center">
						<img
							v-for="estrella in props.data.estrellas"
							:key="estrella"
							src="/assets/img/home/estrella_llena.png"
							alt="Estrella calificada"
							class="estrella"
						/>
						<img
							v-for="estrella in 5 - props.data.estrellas"
							:key="estrella"
							src="/assets/img/home/estrella_vacia.png"
							alt="Estrella sin calificar"
							class="estrella"
						/>
					</div>
				</div>
			</template>
		</Carousel>
		<div class="flex flex-wrap gap-2 justify-content-center align-items-center">
			<a aria-label="Ir a WhatsApp" class="icon" target="_blank" href="https://api.whatsapp.com/send?phone=573176205370">
				<img src="/assets/img/login/wsp.png" alt="WhatsApp" width="42" height="34" />
			</a>
			<a aria-label="Ir a Instagram" class="icon" target="_blank" href="https://www.instagram.com/samyflw1/">
				<img src="/assets/img/login/ins.png" alt="Instagram" width="42" height="34" />
			</a>
			<a aria-label="Ir a TikTok" class="icon" target="_blank" href="https://www.tiktok.com/@samyflw">
				<img src="/assets/img/login/tkk.png" alt="TikTok" width="42" height="34" />
			</a>
		</div>
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
				estrellas: 5,
			},
			{
				nombre: "Luis",
				foto: "/assets/img/perfil2.jpg",
				descripcion: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed euismod, ipsum id malesuada sagittis, mauris velit",
				estrellas: 4,
			},
			{
				nombre: "Pedro",
				foto: "/assets/img/perfil3.jpg",
				descripcion: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed euismod, ipsum id malesuada sagittis, mauris velit",
				estrellas: 3,
			},
			{
				nombre: "Maria",
				foto: "/assets/img/perfil1.jpg",
				descripcion: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed euismod, ipsum id malesuada sagittis, mauris velit",
				estrellas: 2,
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
img.estrella {
	width: 34px;
	height: 34px;
}
.foto_container {
	left: calc(50% - 50px);
	top: -41px;
	width: 100px;
	height: 100px;
	border: 3px solid #25e007;
	padding: 4px;
	border-radius: 50%;
}
.foto_container > img {
	width: 100%;
	height: 100%;
}
.item_resena_usuario {
	max-width: 350px;
	min-width: 350px;
	border: 3px solid #ffffff;
	border-radius: 12px;
	padding: 0 6px 28px 6px;
	z-index: 1;
}
.item_resena_usuario > h3 {
	margin-top: 70px !important;
}

@media (max-width: 450px) {
	.item_resena_usuario {
		max-width: 300px !important;
		min-width: 300px !important;
	}
}
@media (max-width: 300px) {
	img.estrella {
		width: 24px !important;
		height: 24px !important;
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
.resenas > .resenas_usuarios > .p-carousel-content > ul.p-carousel-indicators > li.p-carousel-indicator > button {
	width: 18px;
	height: 18px;
	border-radius: 50%;
}
.resenas > .resenas_usuarios > .p-carousel-content > ul.p-carousel-indicators > li.p-carousel-indicator.p-highlight > button {
	background-color: #25e007;
}
</style>