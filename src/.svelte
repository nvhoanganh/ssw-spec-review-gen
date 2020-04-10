<script>
  export let label;
  export let value;
  export let required = true;
  export let placeholder = '';
</script>

<style>

</style>

<main>
  <label
    class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">
    {label}
  </label>
  <input
    class="appearance-none block w-full text-gray-700 border border-gray-300
    rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white
    focus:border-gray-500"
    {placeholder}
    class:border-red-300={required && !value}
    class:focus:border-red-500={required && !value}
    bind:value
    type="text" />
  {#if required && !value}
    <p class="text-red-500 text-xs italic">This field is required</p>
  {/if}
</main>
