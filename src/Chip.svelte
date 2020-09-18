<script>
  import XIcon from "./XIcon.svelte";
  import {fade} from 'svelte/transition'

  export let value = "";
  export let onDelete = null;
  export let color = "gray";
  export let outline = false;
  export let rounded = "full";
  export let tr_duration= 200
  let klass = "";	

  export { klass as class };

  export let size = "xs";

  let text_c, bg_c, border_c;

  $: if (outline) {
    text_c = color + "-700";
    bg_c = color + "-100";
    border_c = color + "-300";
  } else {
    text_c = color + "-100";
    bg_c = color + "-700";
    border_c = bg_c;
  }

  let size_map = { xs: 6, sm: 8, md: 10, lg: 12, xl: 12 };
  let size_map_icon = { xs: 3, sm: 4, md: 5, lg: 5, xl: 5 };
</script>

<div transition:fade={{duration: tr_duration}}
  class="flex justify-center items-center m-1 font-medium py-1 px-2 bg-white
  rounded-{rounded} text-{text_c} bg-{bg_c} border border-{border_c}
  {klass}">
  <slot name="avatar" />
  <div
    class="text-{size} font-normal {size == 'xs' ? 'leading-none' : ''}
    max-w-full flex-initial">
    <slot>{value}</slot>
  </div>
  {#if onDelete}
    <div class="flex flex-auto flex-row-reverse">
      <div on:click={onDelete}>
        <XIcon
          class="cursor-pointer hover:text-{color}-400 rounded-full w-{size_map_icon[size]}
          h-{size_map_icon[size]} ml-2" />
      </div>
    </div>
  {/if}
</div>
