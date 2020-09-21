<script>
  import { createEventDispatcher } from 'svelte';

  export let title = null;
  export let text = null;
  export let html = null;
  export let active = false;

  export let left = false;
  export let right = false;
  export let top = false;
  export let bottom = false;

  const dispatch = createEventDispatcher();

  const handleMouseOut = () => {
    dispatch('dismiss');
  }
</script>

<style>
  .bubble :global(a, a:visited) {
      z-index: 99;
      color: #FFFFFF;
      text-decoration: none;
  }

  .bubble :global(a:hover) {
    z-index: 99;
    text-decoration: underline;
  }

  .bubble :global(h4, p) {
    font-size: 14px;
    letter-spacing: 0;
    line-height: 24px;
  }

  .bubble :global(h4) {
    text-transform: none;
  }

  .bubble :global(p) {
    font-weight: 500;
  }

  .bubble__wrap {
    position: absolute;
    opacity: 0;
    visibility: hidden;
  }
  
  .bubble {
    font-family: 'Montserrat', 'Poppins', sans-serif;
    font-size: 14px;
    letter-spacing: 0;
    line-height: 24px;
    background-color: #6AB42D;
    width: 30em;
    text-align: center;
    border-radius: 5px;
    color: #FFFFFF;
    margin: 0;
    padding: 0.6em;
    z-index: 97;
  }

  .bubble h4, .bubble p {
    margin: 0;
    color: #FFFFFF;

  }

  .bubble h4 + .bubble p {
    margin-top: 0.6em;
  }

  .bubble::after {
    content: '';
    position: absolute;
    border: 0.7em solid transparent;
    width: 0;
    height: 0;
  }

  .top::after {
    top: 0;
    left: 50%;
    border-bottom-color: #6AB42D;
    border-top: 0;
    margin-left: -0.7em;
    margin-top: -0.7em;
  }

  .bottom::after {
    bottom: 0;
    left: 50%;
    border-top-color: #6AB42D;
    border-bottom: 0;
    margin-left: -0.7em;
    margin-bottom: -0.7em;
  }

  .letf::after {
    left: 0;
    top: 50%;
    border-right-color: #6AB42D;
    border-left: 0;
    margin-top: -0.7em;
    margin-left: -0.7em;
  }

  .right::after {
    right: 0;
    top: 50%;
    border-left-color: #6ab42d;
    border-right: 0;
    margin-top: -0.5em;
    margin-right: -0.5em;
  }

  .active {
    opacity: 1;
    visibility: visible;
  }
</style>

<section>
  <slot />
  <section class:active class="bubble__wrap" on:mouseleave={handleMouseOut}>
    <aside class="bubble" class:top class:bottom class:left class:right>
      {#if title}
      <h4>{title}</h4>
      {/if}
      {#if text}
      <p>{text}</p>
      {:else if html}
      <p>{@html html}</p>
      {/if}
    </aside>  
  </section>
</section>
