<script>
  import "../app.css";
  import SideBar from "./componnents/sideBar.svelte"; 
</script>

<div class="grid grid-cols-12 min-h-screen flex ...">
  <div class="col-span-4 md:col-span-3">
      <SideBar >
        <!-- <a href="/">Home</a>
        <a href="/exercise">Exercise</a>
        <a href="/workout">Workout</a> -->
      </SideBar>
  </div>
  <div class="col-span-8 md:col-span-9 bg-cyan-100 bg-gradient-to-r from-cyan-400 to-cyan-100">
    <section>
      <slot />
    </section>
  </div>
</div>

<style lang="postcss">
  /* Add your styling here */
</style>
