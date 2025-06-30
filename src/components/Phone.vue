<template>
	<div class="nosotros relative h-full">
		<div ref="info_nosotros" class="flex flex-wrap justify-content-evenly row-gap-4 w-full py-5">
			<div class="destacado relative">
				<div class="flex flex-column gap-0">
					<div class="flex flex-wrap gap-4 align-items-center">
						<div class="carta-resaltar"></div>
						<div class="carta-no-resaltar"></div>
					</div>
					<div class="flex flex-wrap gap-4 align-items-center">
						<div class="carta-no-resaltar"></div>
						<div class="carta-resaltar"></div>
					</div>
				</div>
				<Image src="/assets/img/logo_app.png" class="absolute falcon" width="100%" height="100%" alt="Logo App" />
			</div>
			<div class="informacion flex flex-column md:w-4 p-2">
				<h3 class="font-montserrat uppercase text-6xl mb-0">¿QUIÉNES SOMOS?</h3>
				<p class="font-montserrat text-lg">
					Lorem ipsum dolor sit amet consectetur adipisicing elit. Consectetur, ducimus itaque reprehenderit hic quisquam fugiat quas
					aperiam assumenda qui eum. Neque molestias reprehenderit ipsum consectetur corrupti sed distinctio esse illum.
				</p>
				<div class="wrapper w-max">
					<button class="btn-saber-mas text-white font-montserrat text-3xl font-bold relative cursor-pointer">SABER MÁS</button>
				</div>
			</div>
		</div>
	</div>
</template>
<script>
export default {
	data: () => ({
		heightNosotros: 700,
		timeoutHeight: null,
	}),
	mounted() {
		//Esperamos que el DOM cargue todo
		this.$nextTick(() => {
			this.timeoutHeight = setTimeout(() => {
				const info_nosotros = this.$refs.info_nosotros;
				this.heightNosotros = info_nosotros.offsetHeight + 150;
				if (this.timeoutHeight != null) {
					clearTimeout(this.timeoutHeight);
					this.timeoutHeight = null;
				}
			}, 100);
		});
	},
};
</script>
<style scoped>
.nosotros {
	background: radial-gradient(50% 50% at 50% 50%, #5cadbf 0%, #264157 100%);
}
.destacado > .falcon {
	left: calc(50% - 150px);
	top: calc(50% - 175px);
	width: 300px;
	height: 350px;
	user-select: none;
}
.destacado .carta-resaltar {
	width: 275px;
	height: 346px;
	border-radius: 12px;
	background: #ffffff;
}
.destacado .carta-no-resaltar {
	width: 275px;
	height: 239px;
	background: #d9d9d9;
	border-radius: 12px;
}
.informacion > h3 {
	font-weight: 900;
}
.wrapper {
	display: inline-block;
	position: relative;
	filter: drop-shadow(5px 6px 0 white);
}
.informacion > .wrapper > .btn-saber-mas {
	padding: 8px 20px;
	text-align: start;
	width: 250px;
	height: 60px;
	border: none;
	background: #5cadbf;
	clip-path: polygon(0 0, 100% 0, 100% 0, 76% 100%, 0 100%);
}

@media (max-width: 950px) {
	.nosotros > div {
		flex-direction: column !important;
		align-items: center;
	}
	.nosotros .informacion {
		width: 100% !important;
		align-items: center;
	}
	.informacion > h3 {
		margin-top: 0 !important;
		text-align: center;
	}
}
@media (max-width: 850px) {
	.destacado > .falcon {
		top: calc(50% - 249px);
	}
}
@media (max-width: 585px) {
	.destacado > div {
		row-gap: 12px !important;
	}
	.destacado > div > * {
		flex-direction: column;
	}
	.destacado > .falcon {
		top: calc(50% - 178px);
	}
}

@media (max-width: 310px) {
	.destacado > .falcon {
		top: calc(50% - 150px);
		left: calc(50% - 100px);
		width: 200px !important;
		height: 300px !important;
	}
}
@media (max-width: 280px) {
	.destacado .carta-resaltar,
	.destacado .carta-no-resaltar {
		width: 250px !important;
	}
}
</style>