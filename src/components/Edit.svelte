<script lang="ts">
  import 'two-up-element'
  import { originalImage } from '../store';
</script>

<two-up>
  <img src={$originalImage} alt="Original Image" />
  <img  alt="Edited Image" />
</two-up>
