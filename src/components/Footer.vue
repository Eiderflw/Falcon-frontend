<template>
	<footer class="footer w-full flex flex-column align-items-center py-4 text-center word-break">
		<h1 class="text-5xl font-inter mb-1 font-bold uppercase text-xl">Métodos de pago</h1>
		<div class="flex flex-wrap gap-3 justify-content-center align-items-start">
			<img v-for="(marca, index) in marcas_usadas" :src="marca" :key="index" class="marca" alt="Logo marca" />
		</div>
	</footer>
</template>
<script>
export default {
	data: () => ({
		marcas_usadas: ["/assets/img/footer/logo_binance.png", "/assets/img/footer/logo_openpay.png"],
	}),
};
</script>
<style scoped>
.footer {
	background-repeat: no-repeat;
	background-size: 100% 100%;
	background: #eae9e6;
}
.footer > h1 {
	background: linear-gradient(90deg, #5cadbf 0%, rgba(30, 101, 114, 0.71) 100%);
	-webkit-background-clip: text;
	-webkit-text-fill-color: transparent;
	background-clip: text;
	color: transparent;
}
.footer .marca{
	width:180px;
	object-fit: contain;
}
</style>
