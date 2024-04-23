<script lang="ts">
    import { onMount } from 'svelte';
    import axios from 'axios';
    let userProfile: string | null = null;

    const fetchUserProfile = async () => {
        const token = localStorage.getItem('token');
        if (!token) {
            return;
        }

        try {
            const res = await fetch('http://localhost:8080/api/v1/authorized/user/avatar/me', {
                method: 'GET',
                headers: {
                    Authorization: `Bearer ${token}`
                }
            });

            if (!res.ok) {
                throw new Error('Failed to fetch user profile');
            }

            const blob = await res.blob();
            userProfile = URL.createObjectURL(blob); // Update userProfile with the URL of the fetched image
        } catch (error) {
            console.error(error);
        }
    };

    const selectedFile = async () => {
        const fileInput = document.getElementById("restaurantImage") as HTMLInputElement | null;
        if (!fileInput) {
            console.error("File input element not found");
            return;
        }

        fileInput.addEventListener("change", async function () {
            const selectedFile = this.files?.[0];
            const token = localStorage.getItem("token");
            if (selectedFile) {
                try {
                    const formData = new FormData();
                    formData.append("image", selectedFile);
                    const response = await axios.put(
                        "http://localhost:8080/api/v1/authorized/user/avatar/me",
                        formData,
                        {
                            headers: {
                                "Content-Type": "multipart/form-data",
                                Authorization: `Bearer ${token}`,
                            },
                        }
                    );
                    alert("File uploaded successfully");
                    console.log("File uploaded successfully:", response.data);
                    fetchUserProfile(); // Fetch updated user profile after uploading new image
                    fileInput.value = ""; // Reset file input
                } catch (error) {
                    console.error("Error uploading file:", error);
                }
            } else {
                console.log("No file selected");
            }
        });
    };

    onMount(() => {
        fetchUserProfile();
        selectedFile(); // Call selectedFile to add event listener for file input
    });
</script>

<div>
    <!-- Component -->
    <div class="p-8 flex justify-center items-center min-h-screen bg-white">
        <div
            class="w-full md:w-1/2 relative grid grid-cols-1 md:grid-cols-3 border border-gray-300 bg-gray-100 rounded-lg"
        >
            <div
                class="rounded-l-lg p-4 bg-gray-200 flex flex-col justify-center items-center border-0 border-r border-gray-300"
            >
                <label
                    class="cursor-pointer hover:opacity-80 inline-flex items-center shadow-md my-2 px-2 py-2 bg-gray-900 text-gray-50 border border-transparent
                rounded-md font-semibold text-xs uppercase tracking-widest hover:bg-gray-700 active:bg-gray-900 focus:outline-none
               focus:border-gray-900 focus:ring ring-gray-300 disabled:opacity-25 transition ease-in-out duration-150"
                    for="restaurantImage"
                >
                    Select image
                    <input id="restaurantImage" class="text-sm cursor-pointer w-36 hidden" type="file" />
                </label>
            </div>
            <div
                class="relative order-first md:order-last h-28 md:h-auto flex justify-center items-center border border-dashed border-gray-400 col-span-2 m-2 rounded-lg bg-no-repeat bg-center bg-origin-padding bg-cover"
            >
                <span class="text-gray-400 opacity-75">
                    {#if userProfile === null}
                        <svg
                            class="w-14 h-14"
                            xmlns="http://www.w3.org/2000/svg"
                            fill="none"
                            viewBox="0 0 24 24"
                            stroke-width="0.7"
                            stroke="currentColor"
                        >
                            <path
                                stroke-linecap="round"
                                stroke-linejoin="round"
                                d="M2.25 15.75l5.159-5.159a2.25 2.25 0 013.182 0l5.159 5.159m-1.5-1.5l1.409-1.409a2.25 2.25 0 013.182 0l2.909 2.909m-18 3.75h16.5a1.5 1.5 0 001.5-1.5V6a1.5 1.5 0 00-1.5-1.5H3.75A1.5 1.5 0 002.25 6v12a1.5 1.5 0 001.5 1.5zm10.5-11.25h.008v.008h-.008V8.25zm.375 0a.375.375 0 11-.75 0 .375.375 0 01.75 0z"
                            />
                        </svg>
                    {:else}
                        <img src={userProfile} alt="User profile" class="w-full h-full rounded-lg" />
                    {/if}
                </span>
            </div>
        </div>
    </div>
</div>

<style>
    /* Add your CSS styles here */
</style>
