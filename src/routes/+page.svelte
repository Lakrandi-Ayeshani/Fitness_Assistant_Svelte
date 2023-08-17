<!-- <script>
  import { Router, Route, Link } from "svelte-routing";
	import SideBar from "./componnents/sideBar.svelte";
	import Exercise from "./pages/Exercise.svelte";
	import Content from "./pages/content.svelte";
	import About from "./pages/About.svelte";
	import Workout from "./pages/Workout.svelte";
	import AddForm from "./pages/AddForm.svelte";
</script>

  <div class="grid grid-cols-12 min-h-screen flex ...">
    <div class="col-span-4 md:col-span-3">
      <SideBar />
    </div>
    <div class="col-span-8 md:col-span-9 bg-cyan-100">
      <Router>
        <Route path="/" component={Content} />
        <Route path="/exercise" component={Exercise} />
        <Route path="/about" component={About} />
      </Router>
      <AddForm />
    </div>
  </div>
  
  <style lang="postcss">
  </style> -->

<!-- src/routes/ModalExample.svelte -->

<script>
</script>

<div class="bg-gradient-to-r from-cyan-200 to-cyan-400 min-h-screen flex items-center justify-center p-5">
  <div class="text-center">
    <h1 class="text-cyan-800 font-serif italic font-bold text-4xl mb-4">Hello Cloud Parallax</h1>
    <p class="text-cyan-700 font-serif italic text-1xl ">
      This is my web application built with SvelteKit and Tailwind CSS.
      It connects to a NodeJS backend via a RESTful API.
      CRUD functionality is implemented for backend resources. 
    </p>
  </div>
</div>

<style>
</style>
