<script lang="ts">
  import Spinner from "./Spinner.svelte";

  export let disabled: boolean | undefined = undefined;
  export let loading: boolean | undefined = undefined;

  export let type: "submit" | "button" = "button";
  export let variant: "primary" | "danger" | "brand" = "primary";
</script>

<button class={variant} class:loading on:click {disabled} {type}>
  {#if loading}
    <Spinner size={16} />
  {/if}

  <slot />
</button>

<style lang="scss">
  button {
    border: 1px solid transparent;
    border-radius: 0.25rem;
    cursor: pointer;
    display: flex;
    gap: 6px;
    align-items: center;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    padding: 0.375rem 0.75rem;

    &:disabled {
      opacity: 0.3;
      cursor: not-allowed;
    }

    &.loading {
      opacity: 0.3;
      cursor: progress;
    }
  }

  .brand {
    background: #ea580c;
    color: #f8fafc;
  }

  .primary {
    background: #111827;
    color: #f8fafc;
  }

  .danger {
    background: #dc2626;
    color: #fecaca;
  }
</style>
