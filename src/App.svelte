<script lang="ts">
  import Edit from './components/Edit.svelte';
  import Upload from './components/Upload.svelte';
  import { imageStatus } from './store';
  import { ImageStatus } from '../types.d';
</script>


<main class="flex flex-col w-full items-center gap-80">
  <header class="text-4xl font-semibold">
    <h1>Remove the <span class="text-purple-700">Background</span></h1>
  </header>
  
  {#if $imageStatus === ImageStatus.READY || $imageStatus === ImageStatus.UPLOADING }
    <Upload />
  {/if}

  {#if $imageStatus === ImageStatus.DONE}
    <Edit />
  {/if}

  <!-- {#if $imageStatus === ImageStatus.ERROR}
    <div class="flex flex-col items-center gap-4">
      <img src={svelteLogo} alt="Svelte Logo" class="w-40" />
      <h2 class="text-2xl font-semibold">Something went wrong</h2>
      <p class="text-center">Please try again later</p>
    </div>
  {/if} -->

  <footer>Footer</footer>
</main>

