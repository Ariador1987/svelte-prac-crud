<script>
	import { slide } from 'svelte/transition';
	import { fly, blur, fade } from 'svelte/transition';
</script>

<div class="modal-container" in:fade out:fade>
    <div class="modal-content">
        <slot><!-- optional fallback --></slot>
    </div>
</div>