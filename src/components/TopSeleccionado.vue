<template>
	<Panel>
		<template #header>
			<div class="flex align-items-center gap-2 flex-end w-full justify-content-between flex-wrap">
				<h1 class="m-0">Top Seleccionado</h1>
				<div class="botones flex gap-2 flex-wrap">
					<span class="p-input-icon-left">
						<i class="pi pi-search" />
						<InputText v-model="filtersTop['global'].value" placeholder="Buscar..." />
					</span>
					<Button label="Guardar Top seleccionado" icon="pi pi-save" :disabled="btnGuardar" @click="guardarTopSeleccionado" />
				</div>
			</div>
		</template>
		<DataTable
			:value="creadores"
			:filters="filtersTop"
			sortField="diamantes_mes_actual"
			:sortOrder="-1"
			paginator
			:rows="10"
			:rowsPerPageOptions="[5, 10, 20, 50]"
			tableStyle="min-width: 100%"
			dataKey="_id"
			v-model:selection="topSeleccionados"
		>
			<template #header>
				<p class="m-0 text-center text-xl">
					{{ topSeleccionados.length }} {{ topSeleccionados.length == 1 ? "creador seleccionado" : "creadores seleccionados" }}
				</p>
			</template>
			<Column selectionMode="multiple" headerStyle="width: 3rem">
				<template #header>
					<label for="p-checkbox-input" class="mx-1 flex-order-1">Seleccionar</label>
				</template>
			</Column>
			<Column field="usuario" header="Creador" sortable />
			<Column field="agencia" header="Agencia" sortable />
			<Column field="diamantes_mes_actual" header="Diamantes mes" sortable />
			<Column field="diamantes_mes_anterior" header="Diamantes anterior" sortable />
		</DataTable>
	</Panel>
</template>
<script>
import axios from "axios";
import { useStoreEvento } from "../store";
import { FilterMatchMode, FilterOperator } from "primevue/api";
export default {
	data: () => ({
		API: import.meta.env.VITE_APP_API,
		token: {
			headers: {
				Authorization: null,
			},
		},
		store: null,
		filtersTop: {
			global: { value: null, matchMode: FilterMatchMode.CONTAINS },
			name: { operator: FilterOperator.AND, constraints: [{ value: null, matchMode: FilterMatchMode.STARTS_WITH }] },
		},
		btnGuardar: false,
		creadores: [],
		topSeleccionados: [],
	}),
	methods: {
		async getCreadoresAgencia() {
			await axios
				.get(`${this.API}/usuario/agencias`, this.token)
				.then((resp) => {
					this.creadores = resp.data;
				})
				.catch((error) => {
					switch (error.response.data.statusCode) {
						case 401:
							//Se le termino la sesión
							this.store.clearUser();
							this.$router.push("/login");
							break;
						default:
							this.$toast.add({
								severity: "error",
								summary: "Obtener creadores",
								detail: "Sucedió un error, Comuniquese con soporte",
								life: 1500,
							});
							console.log("Error: ", error);
							break;
					}
				});
		},
		async guardarTopSeleccionado() {
			this.btnGuardar = true;
			const seleccionados = this.topSeleccionados.flatMap((top) => top._id);
			await axios
				.post(`${this.API}/top-seleccionado/crear`, seleccionados, this.token)
				.then((resp) => {
					this.$toast.add({
						severity: resp.data.error ? "error" : "success",
						summary: "Top seleccionado",
						detail: resp.data.message,
						life: 1600,
					});
					this.getTopSeleccionados();
				})
				.catch((error) => {
					switch (error.response.data.statusCode) {
						case 401:
							//Se le termino la sesión
							this.store.clearUser();
							this.$router.push("/login");
							break;
						default:
							this.$toast.add({
								severity: "error",
								summary: "Guardar Top seleccionado",
								detail: "Sucedió un error, Comuniquese con soporte",
								life: 1500,
							});
							console.log("Error: ", error);
							break;
					}
				});
			this.btnGuardar = false;
		},
		async getTopSeleccionados() {
			await axios
				.get(`${this.API}/top-seleccionado`, this.token)
				.then((resp) => {
					this.topSeleccionados = resp.data && Array.isArray(resp.data.seleccionado) ? resp.data.seleccionado: [];
				})
				.catch((error) => {
					switch (error.response.data.statusCode) {
						case 401:
							//Se le termino la sesión
							this.store.clearUser();
							this.$router.push("/login");
							break;
						default:
							this.$toast.add({
								severity: "error",
								summary: "Obtener Top seleccionado",
								detail: "Sucedió un error, Comuniquese con soporte",
								life: 1500,
							});
							console.log("Error: ", error);
							break;
					}
				});
		},
	},
	async created() {
		this.store = useStoreEvento();
		if (!this.store.isActive()) {
			this.$router.push("/login");
		}
		this.token.headers.Authorization = `Bearer ${this.store.getToken()}`;
		await this.getTopSeleccionados();
		await this.getCreadoresAgencia();
	},
};
</script>