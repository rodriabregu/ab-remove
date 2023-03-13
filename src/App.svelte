<script lang="ts">
  import Edit from './components/Edit.svelte';
  import Upload from './components/Upload.svelte';
  import { imageStatus } from './store';
  import { ImageStatus } from '../types.d';
</script>

<main class="flex flex-col w-full items-center gap-10 max-w-xl mx-auto">
  <header class="text-4xl font-semibold mt-4">
    <h1>Remove the <span class="text-purple-700">Background</span></h1>
  </header>

  {#if $imageStatus === ImageStatus.READY || $imageStatus === ImageStatus.UPLOADING}
    <Upload />
  {/if}

  {#if $imageStatus === ImageStatus.DONE}
    <Edit />
  {/if}
</main>

<footer class="absolute bottom-0 w-full text-center text-gray-500 text-sm py-4">
  Footer
</footer>
