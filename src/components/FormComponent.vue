<template>
	<v-col cols="11" sm="11" md="4" lg="4">
		<br />
		<br />
		<br />
		<br />
		<br />
		<div class="form">
			<h2>User Form</h2>
			<br />
			<form @submit.prevent="onSubmit">
				<v-text-field
					prepend-icon="mdi-contacts-outline"
					label="Full Name"
					placeholder="Full Name"
					outlined
					dense
					v-model="user.name"
					required
				></v-text-field>

				<v-text-field
					prepend-icon="mdi-account-circle-outline"
					label="Avatar Link"
					placeholder="Avatar Link"
					outlined
					dense
					v-model="user.avatar"
					required
				></v-text-field>
				<v-textarea
					prepend-icon="mdi-account-edit-outline"
					outlined
					placeholder="User Details ..."
					name="input-7-4"
					label="User Details"
					v-model="user.details"
					required
				></v-textarea>

				<v-btn type="submit" outlined medium color="primary" block>Save</v-btn>
				<br />
				<v-btn
					outlined
					medium
					color="warning"
					block
					@click="onClear"
					v-if="isediting"
					>Clear Form</v-btn
				>
			</form>
		</div>
	</v-col>
</template>

<script>
	export default {
		props: ["user", "isediting"],
		data: () => ({}),
		methods: {
			onSubmit(e) {
				this.$emit("save");
			},
			onClear() {
				this.$emit("clear");
			},
		},
	};
</script>

<style scoped>
	.form {
		padding: 20px;
		text-align: center;
	}

	h2 {
		color: #1976d2;
	}
</style>
