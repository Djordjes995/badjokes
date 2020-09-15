<template>
	<div class="main-content">
		<b-container v-if="categories">
			<b-row v-if="!chosenCategory">
				<b-col col lg="4" sm="12" v-for="(category, index) in categories" :key="index">
					<category-item :data="category" @click.native="chooseCategory(category)"></category-item>
				</b-col>
			</b-row>
			<div v-else>
				<div class="content-header">
					<p @click="refresh()" class="back">← Back to categories</p>
					<div class="pages">
						<span
							class="page-no"
							v-for="page in Math.ceil(chosenCategory.jokes.length/pagination)"
							:key="page"
							@click="choosePage(page)"
							:class="chosenPage===page && 'active'"
						>{{page}}</span>
					</div>
					<div class="pagination">
						Jokes per page:
						<select v-model="pagination" @change="resetPage()">
							<option disabled value>Jokes per page</option>
							<option>5</option>
							<option>10</option>
							<option selected>15</option>
						</select>
					</div>
				</div>
				<b-row class="jokes-row">
					<b-col
						cols="12"
						lg="4"
						v-for="joke in chosenCategory.jokes.slice((chosenPage-1)*pagination,chosenPage*pagination)"
						:key="joke.id"
					>
						<joke-item :data="joke" @click.native="openJoke(joke)"></joke-item>
					</b-col>
				</b-row>
			</div>
		</b-container>
		<joke-modal v-if="modal" @close="modal=false">
			<div slot="body">
				<p v-if="chosenJoke.type==='single'">{{chosenJoke.joke}}</p>
				<div v-else>
					<p>
						<span style="font-weight:500;">Get ready:</span>
						{{chosenJoke.setup}}
					</p>
					<p>
						<span style="font-weight:500;">Here it comes:</span>
						{{chosenJoke.delivery}}
					</p>
				</div>
			</div>
		</joke-modal>
	</div>
</template>

<script>
	import CategoryItem from "./CategoryItem";
	import JokeItem from "./JokeItem";
	import JokeModal from "./JokeModal";
	import axios from "axios";

	export default {
		name: "MainContent",
		components: {
			CategoryItem,
			JokeItem,
			JokeModal,
		},
		data() {
			return {
				categories: null,
				allJokes: null,
				chosenCategory: null,
				chosenJoke: null,
				modal: false,
				pagination: 15,
				chosenPage: 1,
			};
		},
		created() {
			axios.get("https://shopviu.com/badjokes.json").then((response) => {
				this.allJokes = response.data.jokes;
				this.getCategories(response.data.jokes);
				console.log(response.data);
			});
		},
		methods: {
			getCategories(jokes) {
				//sort by category
				let categoryKeys = jokes.reduce((categories, joke) => {
					categories[joke.category] = categories[joke.category] || [];
					categories[joke.category].push(joke);
					return categories;
				}, []);
				let categories = [];
				//remove duplicates
				for (var key in categoryKeys) {
					categories.push({
						name: key,
						jokes: this.removeDuplicates(categoryKeys[key], "id"),
					});
				}
				this.categories = categories;
			},
			chooseCategory(category) {
				this.chosenCategory = category;
			},
			refresh() {
				this.chosenCategory = null;
				this.pagination = 15;
				this.chosenPage = 1;
			},
			resetPage() {
				this.chosenPage = 1;
			},
			removeDuplicates(arr, key) {
				return [...new Map(arr.map((item) => [item[key], item])).values()];
			},
			openJoke(joke) {
				this.modal = true;
				this.chosenJoke = joke;
			},
			choosePage(page) {
				this.chosenPage = page;
			},
		},
	};
</script>

<style lang="scss">
	.main-content {
		margin-top: 4rem;
		.content-header {
			display: flex;
			justify-content: space-between;
			align-items: center;
			.pagination {
				select {
					margin-left: 1rem;
				}
			}
			.page-no {
				background-color: #000;
				color: #fff;
				padding: 0.25rem 1rem;
				margin: 0.2rem;
				cursor: pointer;
				font-weight: 500;
				transition: 0.2s;
				border-radius: 2px;
				&.active {
					background-color: #ff4647;
				}
			}
		}
		.jokes-row {
			margin-top: 4rem;
		}
		.back {
			font-weight: 500;
			cursor: pointer;
			font-size: 1.5rem;
		}
		@media (max-width: 768px) {
			margin-top: 2rem;
			.content-header {
				flex-direction: column;
				.pages {
					margin-bottom: 1rem;
				}
				.pagination {
					margin-bottom: 2rem;
				}
			}
			.jokes-row {
				margin: 1rem 0;
			}
		}
	}
</style>
