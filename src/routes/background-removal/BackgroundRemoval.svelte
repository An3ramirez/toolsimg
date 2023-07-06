<script lang="ts">
  import "two-up-element";
  import StepEdit from "./StepEdit.svelte";
  import StepUpload from "./StepUpload.svelte";

  import { imageStatus } from "../../store";
  import { ImageStatus } from "../../../types.d";
</script>

{#if $imageStatus === ImageStatus.READY || $imageStatus === ImageStatus.UPLOADING}
  <div class="flex flex-wrap">
    <div class="w-full lg:w-1/2 p-6 flex items-center justify-center">
      <div class="text-center">
        <two-up class="border-2 border-gray-300">
          <img
            src="/src/assets/mujer-joven-paisaje_250132-3205.jpg"
            alt="Imagen de muestra con fondo"
          />
          <img
            src="/src/assets/mujer-joven-paisaje_250132-3205-removebg.png"
            alt="Imagen de muestra sin fondo"
          />
        </two-up>
        <div class="max-w-xl mx-auto">
          <h1
            class="font-display font-semibold text-typo mt-4 text-3xl md:text-4xl lg:text-5xl text-center text-gray-700"
          >
            Quita el fondo de tus imágenes
          </h1>
        </div>
      </div>
    </div>
    <div class="w-full lg:w-1/2 p-6">
      <StepUpload />
    </div>
  </div>
{:else if $imageStatus === ImageStatus.DONE}
  <div class="flex items-center justify-center">
    <StepEdit />
  </div>
{/if}
