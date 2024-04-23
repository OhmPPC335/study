<script lang="ts">
	import axios from 'axios';
	import {goto} from '$app/navigation';
	let first_name:string = "";
	let email:string = "";
	let maleBtn:boolean = false;
	let femaleBtn:boolean = false;
	let username:string = "";
	let last_name:string = "";
	let password:string = "";
	let gender:string = "";
	const submit = async () => {
		last_name = first_name.split(' ')[1];
		if (maleBtn) {
			gender = 'Male';
		} else if (femaleBtn) {
			gender = 'Female';
		} else {
			gender = 'Other';
		}
		try {
			await axios
				.post('http://localhost:8080/api/v1/auth/register', {
					first_name: first_name,
					last_name: last_name,
					email: email,
					gender: gender,
					username: username,
					password: password
				})
				.then((res) => {
					if(res.status===400){
						alert("User already exists");
					}else if (res.status === 200) {
						alert("User created successfully");
						goto('/login');
					}else{
						alert("Something went wrong");
					}
				});
		} catch (err) {
			console.log(err);
		}
	};
</script>

<div class="flex items-center justify-center p-12 bg-white">
	<!-- Author: FormBold Team -->
	<!-- Learn More: https://formbold.com -->
	<div class="mx-auto w-full max-w-[550px]">
	
			<div class="-mx-3 flex flex-wrap">
				<div class="w-full px-3 sm:w-1/2">
					<div class="mb-5">
						<label for="name" class="mb-3 block text-base font-medium text-[#07074D]">
							First Name and Last Name
						</label>
						<input
							type="text"
							name="name"
							id="name"
							bind:value={first_name}
							placeholder="First Name and Last Name"
							class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
						/>
					</div>
				</div>
				<div class="w-full px-3 sm:w-1/2">
					<div class="mb-5">
						<label for="email" class="mb-3 block text-base font-medium text-[#07074D]">
							Email
						</label>
						<input
							type="text"
							name="email"
							id="email"
							bind:value={email}
							placeholder="email"
							class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
						/>
					</div>
				</div>
				<div class="w-full px-3 sm:w-1/2">
					<div class="mb-5">
						<label for="username" class="mb-3 block text-base font-medium text-[#07074D]">
							Username
						</label>
						<input
							type="text"
							name="username"
							id="username"
							bind:value={username}
							placeholder="username"
							class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
						/>
					</div>
				</div>
				<div class="w-full px-3 sm:w-1/2">
					<div class="mb-5">
						<label for="password" class="mb-3 block text-base font-medium text-[#07074D]">
							Password
						</label>
						<input
							type="password"
							name="password"
							id="password"
							bind:value={password}
							placeholder="password"
							class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
						/>
					</div>
				</div>
			</div>
			<div class="mb-5">
				<label class="mb-3 block text-base font-medium text-[#07074D]"> Gender </label>
				<div class="flex items-center space-x-6">
					<div class="flex items-center">
						<input type="radio" name="male" id="male" class="h-5 w-5" bind:value={maleBtn}/>
						<label for="male" class="pl-3 text-base font-medium text-[#07074D]"> Male </label>
						
					</div>
					<div class="flex items-center">
						<input type="radio" name="female" id="female" class="h-5 w-5" bind:value={femaleBtn}/>
						<label for="female" class="pl-3 text-base font-medium text-[#07074D]"> Female </label>
					</div>
				</div>
			</div>

			<div>
				<button
					class="hover:shadow-form rounded-md bg-[#6A64F1] py-3 px-8 text-center text-base font-semibold text-white outline-none"
					on:click={submit}
				>
					Submit
				</button>
			</div>
	</div>
</div>

<style></style>
