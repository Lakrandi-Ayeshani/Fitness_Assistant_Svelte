<script>
    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';


    let exerciseData = [];
    let currentPage = 1;
    let itemsPerPage = 7;
    let PaginatedData = [];
    let isModalOpen = writable(false);
    let deleteExercise;


    // Fetch data from the API
    async function fetchData() {
        try {
            const response = await fetch('http://localhost:8000/api/exercise');
            if (response.ok) {
                exerciseData = await response.json();
                getPaginatedData() 

            } else {
                console.error('Failed to fetch data from the API');
            }
        } catch (error) {
            console.error('Error fetching data:', error);
        }
    }
    // Call the fetchData function when the component mounts    
    onMount(fetchData);

    function getPaginatedData() {
        const startIndex = (currentPage - 1) * itemsPerPage;
        const endIndex = startIndex + itemsPerPage;
        PaginatedData = exerciseData.slice(startIndex, endIndex);
    }

    function nextPage() {
        if(exerciseData.length/7 > currentPage ) {
            currentPage++;
            getPaginatedData();
        }
    }

    function previousPage() {
        if (currentPage > 1) {
            currentPage--;
            getPaginatedData()
        }
    }
  
  
    // Function to open the modal
    function openModal(value) {
        isModalOpen.set(true);
        deleteExercise = value;
    }
    
    // Function to close the modal
    function closeModal() {
        isModalOpen.set(false);
    }
    const handleDelete = async (ID) => {
        try {
            const response = await fetch(`http://localhost:8000/api/exercise/${ID}`, {
                method: 'DELETE',
                headers: {
                'Content-Type': 'application/json'
            }
            });
            if (response.ok) {
                isModalOpen.set(false);
                alert("Deteleted successfully");
            } else {
                console.error('Failed to delete data from the API');
            }
        } catch (error) {
            console.error('Error deleting data:', error);
        }
    }
</script>

<div class="m-5">
    <h1 class="text-4xl font-bold text-cyan-700 pt-5">Exercise List</h1>
    <div class="flex justify-end">
        <a href="/exercise/add">
            <button class="rounded-lg bg-cyan-500 text-white font-bold p-2 my-5 hover:bg-sky-600 ..." >+ Add Exercise</button>
        </a>
    </div>
  
    <div class="p-4 bg-cyan-200 rounded-lg">
        <div class="space-y-1">
            <!-- Table Header -->
            <div class="bg-cyan-500 shadow-xl text-white p-2 rounded">
                <div class="grid grid-cols-12 gap-x-4 font-bold text-lg">
                    <div class="col-span-1"></div>
                    <div class="col-span-3">Exercise</div>
                    <div class="col-span-6">Description</div>
                    <div class="col-span-1"></div>
                    <div class="col-span-1"></div>
                </div>
            </div>
    
            <!-- Table Rows -->
            {#each PaginatedData as value (value)}
                <div class="bg-cyan-350 shadow-2xl text-cyan-700 p-4 rounded">
                    <div class="grid grid-cols-12 gap-x-4">
                        <div class="col-span-1 md:flex md:justify-center">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M16.5 8.25V6a2.25 2.25 0 00-2.25-2.25H6A2.25 2.25 0 003.75 6v8.25A2.25 2.25 0 006 16.5h2.25m8.25-8.25H18a2.25 2.25 0 012.25 2.25V18A2.25 2.25 0 0118 20.25h-7.5A2.25 2.25 0 018.25 18v-1.5m8.25-8.25h-6a2.25 2.25 0 00-2.25 2.25v6" />
                            </svg>                      
                        </div>
                        <div class="col-span-3">{value.name}</div>
                        <div class="col-span-6">{value.description}</div>
                        <div class="col-span-1 md:flex md:justify-end">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2.5" stroke="currentColor" class="w-6 h-6 text-green-500 hover:fill-green-500 hover:text-white hover:bg-green-500 hover:rounded">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L10.582 16.07a4.5 4.5 0 01-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 011.13-1.897l8.932-8.931zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0115.75 21H5.25A2.25 2.25 0 013 18.75V8.25A2.25 2.25 0 015.25 6H10" />
                            </svg>              
                        </div>
                        <div class="col-span-1">
                            <!-- svelte-ignore a11y-click-events-have-key-events -->
                            <!-- svelte-ignore a11y-no-static-element-interactions -->
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2.5" stroke="currentColor" class="w-6 h-6 text-red-500 hover:fill-red-500 hover:text-white hover:bg-red-500 hover:rounded"  on:click={() => openModal(value)}>
                                <path stroke-linecap="round" stroke-linejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
                            </svg>
                        </div> 
                    </div>
                </div>
            {/each}
        </div>
            <div class="flex justify-between p-3 pb-0">
                <button class="rounded-lg bg-cyan-500 text-white font-bold hover:bg-sky-600 w-20" on:click={previousPage}>Previous</button>
                <button class="rounded-lg bg-cyan-500 text-white font-bold hover:bg-sky-600 w-20" on:click={nextPage}>Next</button>
            </div>
    </div>
</div>

{#if $isModalOpen}
  <div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
    <div class="bg-white p-6 rounded-lg shadow-md">
      <h2 class="text-lg font-bold mb-2 text-red-500">Do you want to delete this Workout</h2>
      <h1>{deleteExercise.name}</h1>
      <h1>{deleteExercise.description}</h1>
      <div class="mt-4 flex justify-end gap-1">
        <button class="rounded-lg bg-cyan-900 text-white font-bold p-2 my-5 hover:bg-cyan-950 ..." on:click={closeModal}>Close</button>
        <button class="rounded-lg bg-red-500 text-white font-bold p-2 my-5 hover:bg-red-600 ..." on:click={() => handleDelete(deleteExercise._id)}>Delete</button>
      </div>
    </div>
  </div>
{/if}

<style>
    /* Component-specific styles */
</style>
  