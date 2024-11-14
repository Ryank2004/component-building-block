<script>
  import { onMount } from 'svelte';
  import { fly } from 'svelte/transition';

  let filterMenuVisible = false;

  function selectCategory() {
    filterMenuVisible = false;
  }

  function handleClickOutside(event) {
    if (!event.target.closest('.filter_menu') && !event.target.closest('.filter_button')) {
      filterMenuVisible = false;
    }
  }

  onMount(() => {
    document.addEventListener('click', handleClickOutside);
    return () => document.removeEventListener('click', handleClickOutside);
  });
</script>

<button class="filter_button" on:click={() => (filterMenuVisible = !filterMenuVisible)} aria-expanded="{filterMenuVisible}">
  FILTER
</button>

{#if filterMenuVisible}
  <div class="filter_menu" transition:fly="{{ x: -300, duration: 300 }}">
    <button class="category_button" on:click={() => selectCategory()}>BREAST</button>
    <button class="category_button" on:click={() => selectCategory()}>GASTROINTESTINAL</button>
    <button class="category_button" on:click={() => selectCategory()}>GYNAECOLOGY</button>
    <button class="category_button" on:click={() => selectCategory()}>HEAD & NECK</button>
    <button class="category_button" on:click={() => selectCategory()}>LUNG</button>
    <button class="category_button" on:click={() => selectCategory()}>NEURO-ONCOLOGY</button>
    <button class="category_button" on:click={() => selectCategory()}>PROSTATE</button>
    <button class="category_button" on:click={() => selectCategory()}>UROLOGY</button>
  </div>
{/if}

<style>
  .filter_button {
    background-color: var(--primary-color);
    color: white;
    outline: none;
    border: none;
    padding: 15px 30px;
    border-radius: 10px;
    margin: 50px 0 0 50px;
    border: 3px solid var(--primary-color);
  }

  .filter_button:hover {
    background-color: white;
    color: var(--primary-color);
  }

  .filter_menu {
    position: fixed;
    top: 0;
    width: 300px;
    height: 100%;
    background-color: #f9f9f9;
    border-right: 1px solid #ccc;
    box-shadow: 3px 0 5px rgba(0, 0, 0, 0.2);
    overflow-y: auto;
    padding-top: 60px;
  }

  .category_button {
    display: inline-flex;
    padding: 12px 24px;
    border: none;
    background: var(--background-color);
    margin: 12px 40px;
    border-radius: 10px;
    text-align: left;
    cursor: pointer;
  }

  .category_button:hover {
    background-color: var(--primary-color);
    color: white;
  }
</style>
