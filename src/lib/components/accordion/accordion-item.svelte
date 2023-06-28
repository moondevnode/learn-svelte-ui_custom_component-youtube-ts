<script lang="ts">
  import { getContext } from 'svelte'
	import { slide } from 'svelte/transition'

  export let open = true

  const componentId = crypto.randomUUID()
  const collapse = getContext('collapse')
  const activeComponentId = getContext('active')

	function setActive() {
		// update the store value in the context
		$activeComponentId = componentId
	}

	function toggleOpen() {
		open = !open
	}

	function handleClick() {
		// if `collapse` is passed only one item can be active
		collapse ? setActive() : toggleOpen()
	}

	// the accordion item to be open by default
	$: open && collapse && setActive()
	// compare if the active id matches the component id
	$: isActive = $activeComponentId === componentId
	// if `collapse`, set one item as active, otherwise use `open`
	$: isOpen = collapse ? isActive : open

</script>

<div class="accordion-item">
  <button on:click={handleClick} class="accordion-toggle">
    <div class="accordion-title">
      <slot name="title" />
    </div>
    <div 
      class="accordion-caret"
      class:open={isOpen}
    >👉</div>
  </button>
  
  {#if isOpen}
    <div transition:slide class="accordion-content">
      <slot name="content" />
    </div>
  {/if}
</div>

<style>
  .accordion-toggle {
    width: 100%;
    display: flex;
    justify-content: space-between;
    padding: var(--accordion-padding, 1rem);
    color: var(--accordion-color, inherit);
    font: inherit;
    font-weight: 600;
    border: none;
    background: none;
    cursor: pointer;
    border-radius: var(--accordion-radius, 4px);
    transition: background-color 0.1s ease;
  }

  .accordion-toggle:hover {
    background-color: var(--accordion-hover, hsl(220 20% 20%));
  }

  .accordion-caret {
    transition: rotate 0.3s ease;
  }

  .accordion-content {
    padding: var(--accordion-content-padding, 1rem);
  }

  .open {
    rotate: 90deg;
  }
</style>