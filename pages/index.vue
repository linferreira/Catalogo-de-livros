<template>
	<div>
		<v-row>
			<v-col md="4">
				<h2 class="text-center mb-5">Lidos Recentemente</h2>
				<v-row v-for="(item, index) in recentBooks" :key="index">
					<BookCard
						class="mb-5"
						:bookTitle="item.title"
						:bookAuthor="item.author"
						:bookDescription="item.description"
					>
						<template v-slot:button>
							<v-btn @click.stop="edit(item, index)">Edit</v-btn>
							<v-btn @click.stop="remove(item.category, index)"
								>Remove</v-btn
							>
						</template>
					</BookCard>
				</v-row>
			</v-col>
			<v-col md="4">
				<h2 class="text-center mb-5">Favoritos</h2>
				<v-row v-for="(item, index) in favouriteBooks" :key="index">
					<BookCard
						class="mb-5"
						:bookTitle="item.title"
						:bookAuthor="item.author"
						:bookDescription="item.description"
					>
						<template v-slot:button>
							<v-btn @click.stop="edit(item, index)">Editar</v-btn>
							<v-btn @click.stop="remove(item.category, index)"
								>Remover</v-btn
							>
						</template>
					</BookCard>
				</v-row>
			</v-col>
			<v-col md="4">
				<h2 class="text-center mb-5">Só os TOP</h2>
				<v-row v-for="(item, index) in bestOfTheBest" :key="index">
					<BookCard
						class="mb-5"
						:bookTitle="item.title"
						:bookAuthor="item.author"
						:bookDescription="item.description"
					>
						<template v-slot:button>
							<v-btn @click.stop="edit(item, index)">Edit</v-btn>
							<v-btn @click.stop="remove(item.category, index)"
								>Remove</v-btn
							>
						</template>
					</BookCard>
				</v-row>
			</v-col>
		</v-row>
		<BookModal />
	</div>
</template>

<script>
import BookCard from "@/components/BookCard";
import BookModal from "@/components/BookModal";
import { eventBus } from "@/eventBus";

export default {
	components: {
		BookCard,
		BookModal
	},
	data() {
		return {
			recentBooks: [],
			favouriteBooks: [],
			bestOfTheBest: []
		};
	},
	created() {
		eventBus.$on("save-book", cardData => {
			if (cardData.category === "Lidos Recentemente") {
				this.recentBooks.push(cardData);
			}
			if (cardData.category === "Favoritos") {
				this.favouriteBooks.push(cardData);
			}
			if (cardData.category === "Só os TOP") {
				this.bestOfTheBest.push(cardData);
			}
		});
	},

	methods: {
		remove(category, index) {
			if (category === "Lidos Recentemente") {
				this.recentBooks.splice(index, 1);
			}
			if (category === "Favoritos") {
				this.favouriteBooks.splice(index, 1);
			}
			if (category === "Só os TOP") {
				this.bestOfTheBest.splice(index, 1);
			}
		},
		edit(item, index) {
			if (item.category === "Lidos Recentemente") {
				eventBus.$emit("open-add-book-modal", item);
				this.recentBooks.splice(index, 1);
			}
			if (item.category === "Favoritos") {
				eventBus.$emit("open-add-book-modal", item);
				this.favouriteBooks.splice(index, 1);
			}
			if (item.category === "Só os TOP") {
				eventBus.$emit("open-add-book-modal", item);
				this.bestOfTheBest.splice(index, 1);
			}
		}
	}
};
</script>
