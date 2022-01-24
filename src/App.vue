<template>
	<v-app>
		<v-main class="main">
			<v-row justify="center" align="start">
				<FormComponent
					:user="user"
					:isediting="isEditing"
					@save="saveData"
					@clear="clearForm"
				/>
				<UserListComponent
					:users="users"
					@delete="deleteData"
					@edit="editData"
				/>
			</v-row>
		</v-main>
	</v-app>
</template>

<script>
	import FormComponent from "./components/FormComponent.vue";
	import UserListComponent from "./components/UsersListComponent.vue";

	export default {
		name: "App",

		components: {
			FormComponent,
			UserListComponent,
		},

		data: () => ({
			isEditing: false,
			user: {
				name: "",
				avatar: "",
				details: "",
			},
			users: [],
		}),
		methods: {
			clearForm() {
				this.user = {
					name: "",
					avatar: "",
					details: "",
				};
				this.isEditing = false;
			},

			editData(id) {
				this.isEditing = true;
				let user = Object.assign(
					{},
					this.users.find((user) => user.id == id)
				);
				this.user = user;
			},
			deleteData(id) {
				this.users = this.users.filter((user) => user.id != id);
				localStorage.setItem("users", JSON.stringify(this.users));
			},
			saveData() {
				let newUser = Object.assign({}, this.user);

				if (!this.isEditing) {
					newUser.id = parseInt(Math.random() * 101);

					this.users.push(newUser);
				} else {
					let newUsers = Object.assign([], this.users);

					this.users = newUsers.map((user) =>
						user.id == newUser.id ? newUser : user
					);
					this.isEditing = false;
				}
				this.user = {
					name: "",
					avatar: "",
					details: "",
				};
				localStorage.setItem("users", JSON.stringify(this.users));
			},
		},

		mounted() {
			if (localStorage.getItem("users")) {
				this.users = JSON.parse(localStorage.getItem("users"));
				console.log(this.users);
			}
		},
	};
</script>
<style scoped>
	.main {
		background-color: rgb(255, 255, 255);
	}
</style>
