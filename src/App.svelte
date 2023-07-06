<script lang="ts">
  import CloudinaryLogo from "./CloudinaryLogo.svelte";
  import Layout from "./routes/layout.svelte";
  import BackgroundRemoval from "./routes/background-removal/BackgroundRemoval.svelte";
</script>

<header class="justify-center">
  <Layout />
</header>

<div class="m-auto w-full p-6 min-h-screen">
  <main class="block">
    <BackgroundRemoval />
  </main>
</div>

<footer
  class="flex justify-center items-center gap-x-2 font-semibold py-4 bg-gray-200 sticky bottom-0"
>
  Hecho con
  <a href="https://cloudinary.com" target="_blank" rel="noreferrer"
    ><CloudinaryLogo /></a
  >
</footer>
