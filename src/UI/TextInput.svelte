
<script>
export let controlType = null;
export let value
export let id = null
export let label
export let rows = null
export let type = "text"
</script>

 <style>
  .form-control {
    display: grid;
    grid-gap: 5px;
  }
 </style>

<div class="form-control">
  <label for="{id}" >{label}</label>
{#if controlType === 'textarea'}
  <textarea rows="{rows}" id="{id}" value={value} on:input />
{:else}
  <input type="{type || 'text'}" id="{id}" value={value} on:input />
{/if}
</div>