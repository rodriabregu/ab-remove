<script lang="ts">
  import 'two-up-element'
  import { originalImage, processedImage } from '../store';
</script>

<two-up>
  <img src={$originalImage} alt="Original" />
  <img src={$processedImage} alt="Edited" />
</two-up>
