<template>
	<v-col cols="11" sm="11" md="8" lg="4">
		<br />
		<br />
		<br />
		<br />
		<div class="form">
			<h2>List of Users</h2>
			<div class="users" v-if="users.length != 0">
				<br />

				<v-card class="user" v-for="user in users" :key="user.id">
					<v-avatar size="50px">
						<img :src="user.avatar" alt="" />
					</v-avatar>
					<div class="userDetails">
						<h3>{{ user.name }}</h3>
						<p>{{ user.details }}</p>
					</div>
					<v-spacer></v-spacer>
					<div class="buttons">
						<v-btn
							class="ic"
							fab
							dark
							x-small
							color="primary"
							@click="onEdit(user)"
						>
							<v-icon dark> mdi-pencil </v-icon>
						</v-btn>

						<v-btn
							class="ic"
							fab
							dark
							x-small
							color="error"
							@click="onDelete(user)"
						>
							<v-icon dark> mdi-trash-can-outline </v-icon>
						</v-btn>
					</div>
				</v-card>
			</div>

			<div class="empty" v-if="users.length == 0">
				<div class="imgCon">
					<br />
					<img src="../assets/undraw_astronaut_re_8c33.svg" alt="" />
					<h4>There are no saved users yet.</h4>
				</div>
			</div>
			<br />
		</div>
	</v-col>
</template>

<script>
	export default {
		props: ["users"],
		data: () => ({}),

		methods: {
			onDelete(user) {
				this.$emit("delete", user.id);
			},
			onEdit(user) {
				this.$emit("edit", user.id);
			},
		},
	};
</script>

<style scoped>
	.form {
		padding: 40px;
		text-align: center;
	}

	h2,
	h3,
	h4 {
		color: #1976d2;
	}

	h4 {
		padding: 10px;
		font-weight: 300;
	}

	p {
		font-size: 12px;
	}

	.imgCon {
		padding: 20px;
	}
	img {
		width: 250px;
	}

	.user {
		padding: 10px 20px;
		margin: 5px 0px;
		display: flex;
		justify-content: flex-start;
		align-items: center;
		cursor: pointer;
	}

	.userDetails {
		padding: 5px 15px;
		text-align: left;
	}

	.ic {
		margin: 5px;
	}
</style>
