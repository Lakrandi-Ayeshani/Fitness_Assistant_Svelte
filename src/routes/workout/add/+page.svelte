<script>
  async function handleSubmit(event) {
    event.preventDefault();
    const formData = new FormData(event.target);
    const requestData = {
      method: 'POST',
      body: JSON.stringify(Object.fromEntries(formData)),
      headers: {
        'Content-Type': 'application/json'
      }
    };

    try {
      const response = await fetch('http://localhost:8000/api/workout', requestData);
      if (response.ok) {
        alert('workout added successfully');
        event.target.name.value = "";
        event.target.description.value = "";
      } else {
        console.error('Failed to add exercise');
      }
    } catch (error) {
      console.error('Error adding exercise:', error);
    }
}

</script>

<div class="flex justify-center pt-20">
    <div class="m-5 p-3 flex bg-cyan-200 justify-center rounded-lg shadow-2xl ">
        <div class="p-1 bg-cyan-400 rounded-lg">
            <div class="bg-cyan-200 rounded-lg px-10">
                <!-- svelte-ignore a11y-click-events-have-key-events -->
                <!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
                <form on:submit={handleSubmit}>
                    <div class="pb-5">
                        <h1 class="flex justify-center text-3xl font-bold text-cyan-700 pt-10" >Add Workout</h1>
                    </div>
                    <div class="pb-5">
                        <label>
                            <div class="pb-2 text-cyan-700 font-bold">Name</div>
                            <input class="w-80 shadow-lg rounded"  name="name" type="string">
                        </label>
                    </div>
                    <div class="pb-5">
                        <label>
                            <div class="pb-2 text-cyan-700 font-bold">Description</div>
                            <input class="w-80 shadow-lg rounded" name="description" type="string">
                        </label>
                    </div>
                    <div class="flex justify-end gap-1">
                        <button class="rounded-lg bg-cyan-500 text-white font-bold p-2 my-5 hover:bg-sky-600 w-20 shadow-lg ..." type="submit">Add</button>
                        <button class="rounded-lg bg-red-500 text-white font-bold p-2 my-5 hover:bg-red-700 w-20 shadow-lg ..." type="button">Cancel</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</div>

<style>
</style>