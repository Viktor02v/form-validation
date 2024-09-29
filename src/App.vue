<script setup>
import { ref } from 'vue';
import formdata from './formdata.json'; // Imported JSON file

// Reactive form fields
const username = ref('');
const password = ref('');

const isValidated = ref(false);

// Reactive error messages
const usernameError = ref(null);
const passwordError = ref(null);

// Form validation logic
function validateForm() {
	let isValid = true;
	usernameError.value = null;
	passwordError.value = null;

	// Username validation
	if (username.value.length < 5) {
		usernameError.value = 'Username must be at least 5 characters long';
		isValid = false;
	}

	// Password validation
	if (password.value.length < 8) {
		passwordError.value = 'Password must be at least 8 characters long';
		isValid = false;
	} else if (!/[a-zA-Z]/.test(password.value) || !/[0-9]/.test(password.value)) {
		passwordError.value = 'Password must contain both letters and numbers';
		isValid = false;
	}

	isValidated.value = isValid;
}

// Form submission logic
function submitForm() {
	if (validateForm()) {
		// Create formData object
		const newFormData = {
			username: username.value,
			password: password.value,
		};

		// Simulate pushing new data to the existing formdata.json object
		formdata.push(newFormData);

		// Log the updated formdata in the console
		console.log('Updated formdata:', formdata);
	}
}
</script>

<template>
	<div class="window">
	<div v-if="!isValidated" class="form-container">
		<h3>Login Form</h3>
		<form @submit.prevent="submitForm">
			<div>
				<label for="username">Username:</label>
				<input type="text" v-model="username" id="username" placeholder="Enter your username" />
				<div v-if="usernameError" class="error">{{ usernameError }}</div>
			</div>

			<div>
				<label for="password">Password:</label>
				<input type="password" v-model="password" id="password" placeholder="Enter your password" />
				<div v-if="passwordError" class="error">{{ passwordError }}</div>
			</div>

			<button type="submit">Submit</button>
		</form>
	</div>

	<div class="Home">
		Hey there
	</div>
</div>
</template>

<style scoped>
.window {
	background: #ff0404;
	width: full;
	height: 100vh;
}
.form-container {
	position: fixed;
	background: #dcf900;
	width: 100%;
	height: 100%;
	display: flex;
	justify-content: center;
	align-items: center;
	flex-direction: column;
}
</style>