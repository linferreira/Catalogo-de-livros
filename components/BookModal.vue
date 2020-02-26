<template>
	<v-dialog max-width="500px" v-model="open">
		<v-card class="modal">
			<v-card-title>Add Books</v-card-title>
			<v-form>
				<v-select
					v-model="category"
					:items="categories"
					label="Escolha a Categoria"
				></v-select>
				<v-text-field
					v-model="title"
					label="Título do Livro"
				></v-text-field>
				<v-text-field
					v-model="author"
					label="Nome do Autor"
				></v-text-field>
				<v-textarea
					v-model="description"
					label="Descrição do Livro"
				></v-textarea>
			</v-form>
			<v-card-actions>
				<v-spacer></v-spacer>
				<v-btn @click.stop="saveBook" color="#1976D2">Adicionar</v-btn>
			</v-card-actions>
		</v-card>
	</v-dialog>
</template>

<script>
import { eventBus } from "@/eventBus";
export default {
	data() {
		return {
			open: false,
			category: "",
			title: "",
			author: "",
			description: "",
			categories: [
				"Lidos Recentemente",
				"Favoritos",
				"Só os TOP"
			]
		};
	},
	created() {
		eventBus.$on("open-add-book-modal", data => {
			if (data) {
				this.category = data.category;
				this.title = data.title;
				this.author = data.author;
				this.description = data.description;
			}
			this.open = true;
		});
	},
	methods: {
		saveBook() {
			let cardData = {
				title: this.title,
				author: this.author,
				description: this.description,
				category: this.category
			};
			eventBus.$emit("save-book", cardData);
			this.open = false;
		}
	}
};
</script>

<style>
	.modal {
		padding: 10px;
	}
</style>