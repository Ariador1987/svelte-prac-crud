<script>
	import { fly, blur, fade, slide } from 'svelte/transition';
</script>

<div class="modal-container" in:fade out:fade>
    <div class="modal-content" in:fly={{y: 200}} out:fade>
        <slot><!-- optional fallback --></slot>
    </div>
</div>