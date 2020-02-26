<template>
	<v-app dark>
		<v-app-bar :clipped-left="clipped" fixed app>
			<v-toolbar-title v-text="title" />
			<v-spacer />
			<v-btn color="#1976D2" @click.stop="openModal">novo livro</v-btn>
		</v-app-bar>
		<v-content>
			<v-container>
				<nuxt />
			</v-container>
		</v-content>
		<v-footer :fixed="fixed" app>
			<span> &copy; Lindsay Ferreira, 2020</span>
		</v-footer>
	</v-app>
</template>

<script>
import { eventBus } from "@/eventBus";
export default {
	data() {
		return {
			clipped: false,
			drawer: false,
			fixed: false,

			miniVariant: false,
			right: true,
			rightDrawer: false,
			title: "Catálogo de Livros"
		};
	},
	methods: {
		openModal() {
			eventBus.$emit("open-add-book-modal");
		}
	}
};
</script>
