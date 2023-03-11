<script lang="ts">
  import Dropzone from 'dropzone';
  import 'dropzone/dist/dropzone.css';
  import { onMount } from 'svelte';
  import { ImageStatus } from '../../types.d';
  import { imageStatus, originalImage } from '../store';

  onMount(
    () => {
      const dropzone = new Dropzone('#dropzone', {
        // url: 'https://api.cloudinary.com/v1_1/rodriab/image/upload',
        maxFiles: 1,
        acceptedFiles: 'image/*',
        uploadMultiple: false,
        addRemoveLinks: true,
        dictRemoveFile: 'Remove',
        dictDefaultMessage: 'Drop files here to upload',
        dictFallbackMessage: 'Your browser does not support drag\'n\'drop file uploads.',
        dictFileTooBig: 'File is too big ({{filesize}}MiB). Max filesize: {{maxFilesize}}MiB.',
        dictInvalidFileType: 'You can\'t upload files of this type.',
        dictResponseError: 'Server responded with {{statusCode}} code.',
        dictCancelUpload: 'Cancel upload',
        dictCancelUploadConfirmation: 'Are you sure you want to cancel this upload?',
        dictRemoveFileConfirmation: null,
        dictMaxFilesExceeded: 'You can not upload any more files.',
      });

      dropzone.on('sending', (file, xhr, formData) => {
        imageStatus.set(ImageStatus.UPLOADING);
        formData.append('upload_preset', 'llw79me8');
        formData.append('timestamp', (Date.now() / 1000));
        formData.append('api_key', '488249629195227');
      });

      dropzone.on('success', (file, response) => {
        const { secure_url: url } = response;

        imageStatus.set(ImageStatus.DONE);
        originalImage.set(url);
        console.log(response);
      });

      dropzone.on('error', (file, response) => {
        imageStatus.set(ImageStatus.ERROR);
        console.log(response);
      });
      });
</script>

<form id="dropzone" action="https://api.cloudinary.com/v1_1/rodriab/image/upload" class="aspect-video rounded-md border-dashed border-1 border-gray-300 shadow-md flex flex-col items-center p-4">
  {#if $imageStatus === ImageStatus.READY}
  <button class="pointer-events-none bg-violet-500 text-white py-4 px-2 rounded-md text-xl font-bold">Uplaoad files</button>
  <strong class="text-md mt-4">or drop a file</strong>
  {/if}

  {#if $imageStatus === ImageStatus.UPLOADING}
    <strong class="text-md">Uploading...</strong>
  {/if}

  {#if $imageStatus === ImageStatus.ERROR}
    <strong class="text-md">Error</strong>
  {/if}
</form>