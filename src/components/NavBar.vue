<template>
	<div class="navbar">
		<Sidebar v-model:visible="visibleSidebar">
			<Menu :model="itemsMenu" class="w-full">
				<!-- <template #start>
                    <span class="inline-flex items-center gap-1 px-2 py-2 w-full sm:w-[15rem]">
                        <span class="text-2xl font-bold logo"><span>Samy</span>flw</span>
                    </span>
                </template> -->
				<template #submenuheader="{ item }">
					<span class="text-primary-500 dark:text-primary-400 font-bold leading-none">{{ item.label }}</span>
				</template>
				<template #item="{ item, props }">
					<router-link v-if="item.route" v-slot="{ href, navigate }" :to="item.route" custom>
						<a v-ripple :href="href" v-bind="props.action" @click="navigate">
							<span :class="item.icon" />
							<span class="ml-2">{{ item.label }}</span>
						</a>
					</router-link>
				</template>
			</Menu>
		</Sidebar>
		<header class="w-full m-0">
			<div class="opciones flex justify-content-between align-items-center w-full">
				<div class="logo">
					<router-link to="/"><img src="/assets/img/logo_app.png" alt="Logo" class="w-full h-full select-none" /></router-link>
				</div>
				<nav class="font-monomaniac-one">
					<router-link to="/duckracer" class="font-monomaniac-one">Juegos</router-link>
					<router-link to="/terminos" class="font-monomaniac-one">Términos</router-link>
					<router-link to="/actualizaciones-reglas" class="font-monomaniac-one">Control reglas</router-link>
					<router-link to="/evento" class="font-monomaniac-one">Eventos</router-link>

					<router-link to="/login">
						<button class="btn_login cursor-pointer font-bold font-monomaniac-one">INICIA SESIÓN</button>
					</router-link>
					<Button icon="pi pi-bars" class="botonMenu" text size="large" @click="visibleSidebar = true" />
				</nav>
			</div>
		</header>
	</div>
</template>
<script>
export default {
	data: () => ({
		visibleSidebar: false,
		itemsMenu: [
			{
				separator: true,
			},
			{
				label: "Creadores",
				items: [
					{
						label: "Login Agencia",
						icon: "pi pi-users",
						route: "/login",
					},
				],
			},
			{
				label: "Eventos",
				items: [
					{
						label: "Eventos Activos",
						icon: "pi pi-desktop",
						route: "/evento",
					},
				],
			},
			{
				label: "EventosEspeciales",
				items: [
					{
						label: "Eventos Especiales",
						icon: "pi pi-desktop",
						route: "/EventoEspecialView",
					},
				],
			},
			{
				label: "Control Reglas",
				items: [
					{
						label: "Control Reglas",
						icon: "pi pi-sliders-h",
						route: "/actualizaciones-reglas",
					},
				],
			},
			{
				separator: true,
			},
			{
				label: "Juegos",
				items: [
					{
						label: "DuckRacer",
						icon: "pi pi-caret-right",
						route: "/duckracer",
					},
				],
			},
		],
	}),
};
</script>
<style scoped>
.navbar {
	position: fixed !important;
	display: flex;
	top: 20px;
	width: calc(100% - 40px);
	max-width: calc(100vw - 40px);
	left: 20px;
	right: calc(100% - 20px);
	border-radius: 12px;
	flex-direction: column;
	z-index: 10;
	background: #757171;
	background: linear-gradient(80deg, rgba(117, 113, 113, 0.85) 0%, rgba(7, 8, 7, 0.78) 50%);

	border: none;
	border-image: radial-gradient(100% 266.82% at 0% 2.79%, #1e6572 0%, #5cadbf 100%),
		radial-gradient(98.54% 262.92% at 1.46% 0%, #ffffff 0%, rgba(255, 255, 255, 0) 100%),
		radial-gradient(98.54% 262.92% at 0% 0%, #151515 0%, rgba(21, 21, 21, 0) 100%);
	backdrop-filter: blur(42px);
	padding: 2px 12px;
}
.navbar::before {
	content: "";
	position: absolute;
	inset: 0;
	border-radius: 10px;
	background: linear-gradient(90deg, #1e6572b5 0%, #5cadbf 100%) border-box;
	z-index: -1;
	border: 1.9px solid transparent;
	-webkit-mask: linear-gradient(#fff 0 0) padding-box, linear-gradient(#fff 0 0);
	-webkit-mask-composite: xor;
	mask-composite: exclude;
	pointer-events: none;
}

header .logo {
	width: 65px;
	height: 60px;
}

header nav {
	display: flex;
	gap: 15px;
	font-weight: bold;
	color: #ffffff;
	line-height: 100%;
	text-transform: uppercase;
	align-items: center;
}
header nav a {
	font-family: "Monomaniac One";
	vertical-align: middle;
}

.btn_login {
	background-color: #5cadbf;
	color: #1e65727a;
	border-image: linear-gradient(0deg, #5cadbf 1%, white 90%);
	border-image-slice: 1;
	border-width: 2px;
	padding: 4px 16px;
	box-shadow: 6px -5px 6px 0px rgba(92, 173, 191, 0.59);
	-webkit-box-shadow: 6px -5px 6px 0px rgba(92, 173, 191, 0.59);
	-moz-box-shadow: 6px -5px 6px 0px rgba(92, 173, 191, 0.59);
}
.botonMenu {
	display: none;
}
@media (max-width: 739px) {
	header nav a {
		display: none;
	}

	.botonMenu {
		display: flex;
	}
}

header nav a {
	color: #fff;
	font-size: 1.1em;
	text-decoration: none;
}
</style>
