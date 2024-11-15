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
    // return () => document.removeEventListener('click', handleClickOutside);
  });
</script>

<button class="filter_button" on:click={() => (filterMenuVisible = !filterMenuVisible)} aria-expanded="{filterMenuVisible}">
  FILTER <svg class="filter_icon" xmlns="http://www.w3.org/2000/svg" height="20px" viewBox="0 -960 960 960" width="20px" fill="white"><path d="M440-160q-17 0-28.5-11.5T400-200v-240L168-736q-15-20-4.5-42t36.5-22h560q26 0 36.5 22t-4.5 42L560-440v240q0 17-11.5 28.5T520-160h-80Zm40-308 198-252H282l198 252Zm0 0Z"/></svg>
</button>

{#if filterMenuVisible}
  <div class="filter_menu" transition:fly="{{ x: -270, duration: 300 }}">
    <svg class="close_icon" xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960" width="24px" fill="var(--primary-color)"><path d="m256-200-56-56 224-224-224-224 56-56 224 224 224-224 56 56-224 224 224 224-56 56-224-224-224 224Z"/></svg>
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
    display: inline-flex;
    background-color: var(--primary-color);
    color: white;
    align-items: center;
    outline: none;
    border: none;
    padding: 4.75px 10px;
    border-radius: 10px;
    margin: 50px 0 0 50px;
    border: 3px solid var(--primary-color);
  }

  .filter_icon {
    margin-left: 10px;
    font-size: 20px;
  }

  .close_icon {
    margin-left: 230px;
    width: 30px;
    height: 30px;
  }

  .filter_button:hover {
    background-color: white;
    color: var(--primary-color);
  }

  .filter_menu {
    /* display: flex;
    flex-direction: column; */
    position: fixed;
    top: 0;
    width: 270px;
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
