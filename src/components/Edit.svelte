<script lang="ts">
  import 'two-up-element';
  import { originalImage, processedImage } from '../store';

  let processingImage = true;
  let tries = 0;
  let intervalId: number;

  $: {
    if (processingImage) {
      clearInterval(intervalId);
      intervalId = setInterval(() => {
        tries++;
        const img = new Image();
        img.src = $processedImage;
        img.onload = () => {
          processingImage = false;
          clearInterval(intervalId);
        };
      }, 750);
    }
  }
</script>

<two-up>
  <img src={$originalImage} alt="Original" />

  {#if processingImage}
    <div class="flex flex-col items-center gap-4">
      <h2 class="text-2xl font-semibold">Processing image</h2>
      <p class="text-center">Please wait</p>
    </div>
  {:else}
    <img src={$processedImage} alt="Processed" />
  {/if}
</two-up>

<a
  download
  href={$processedImage}
  class="bg-violet-500 text-white py-2 px-2 rounded-md text-xl font-bold"
  >Download image without background</a
>
