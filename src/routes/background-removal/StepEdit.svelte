<script lang="ts">
  import "two-up-element";
  import { originalImage, modifiedImage, imageStatus } from "../../store";
  import { ImageStatus } from "../../../types.d";

  let processingImage = true;
  let tries = 0;
  let intervalId: any;

  $: {
    if (processingImage) {
      clearInterval(intervalId);
      intervalId = setInterval(() => {
        tries++;
        const img = new Image();
        img.src = $modifiedImage;
        img.onload = () => {
          processingImage = false;
          clearInterval(intervalId);
        };

        if (tries >= 60) {
          clearInterval(intervalId);
        }
      }, 1000);
    }
  }

  function toggleState() {
    imageStatus.set(ImageStatus.READY);
  }
</script>

<div class="max-w-4xl">
  {#if processingImage}
    <div>
      <img
        src="https://cdn.dribbble.com/users/902865/screenshots/4814970/loading-opaque.gif"
        alt="Procesando imagen..."
      />
      <div class="flex flex-col justify-center items-center">
        <p class="text-center font-bold text-2xl">Procesando imagen...</p>
      </div>
    </div>
  {:else}
    <two-up>
      <img src={$originalImage} alt="Imagen original subida por el usuario" />
      <img src={$modifiedImage} alt="Imagen sin fondo subida por el usuario" />
    </two-up>
  {/if}

  {#if !processingImage}
    <a
      download
      href={$modifiedImage}
      class="block bg-blue-500 hover:bg-blue-700 text-xl text-center w-full font-bold text-white rounded-full px-4 py-2 mt-10"
    >
      Descargar imagen sin fondo
    </a>

    <button
      on:click={toggleState}
      type="button"
      class="w-full text-gray-900 hover:text-white border border-gray-800 hover:bg-gray-900 focus:ring-4 focus:outline-none focus:ring-gray-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2 dark:border-gray-600 dark:text-gray-400 dark:hover:text-white dark:hover:bg-gray-600 dark:focus:ring-gray-800 mt-3"
      >Atras</button
    >
  {/if}
</div>
