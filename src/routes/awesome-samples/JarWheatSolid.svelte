<script lang='ts'>
  import { getContext } from 'svelte';
  type TitleType = {
    id?: string;
    title?: string;
  };
  type DescType = {
    id?: string;
    desc?: string;
  };
  interface BaseProps {
    size?: string;
    role?: string;
    color?: string;
    withEvents?: boolean;
    onclick?: (event: MouseEvent) => void;
    onkeydown?: (event: KeyboardEvent) => void;
    onkeyup?: (event: KeyboardEvent) => void;
    class?: string;
  }
  interface CtxType extends BaseProps {}
  const ctx: CtxType = getContext('iconCtx') ?? {};
  interface Props extends BaseProps{
    title?: TitleType;
    desc?: DescType;
    ariaLabel?: string;
  }

  let { 
    size = ctx.size || '24', 
    role = ctx.role || 'img', 
    color = ctx.color || 'currentColor', 
    withEvents = ctx.withEvents || false, 
    title = {}, 
    desc = {}, 
    class: classname, 
    ariaLabel =  "jar wheat solid" , 
    onclick, 
    onkeydown, 
    onkeyup,
    ...restProps 
  }: Props = $props();

  let ariaDescribedby = `${title.id || ''} ${desc.id || ''}`;
  let hasDescription = $state(false);

  function updateHasDescription() {
    // Double negation converts truthy values to true, falsy to false
    hasDescription = !!(title.id || desc.id); 
  }
  updateHasDescription();

  $effect(() => {
    updateHasDescription();
  })
</script>

{#if withEvents}
  <svg
    xmlns="http://www.w3.org/2000/svg"
    {...restProps}
    {role}
    width={size}
    height={size}
    class={classname}
    fill={color}
    aria-label={ariaLabel}
    aria-describedby={hasDescription ? ariaDescribedby : undefined}
    viewBox="0 0 320 512"
    onclick={onclick}
    onkeydown={onkeydown}
    onkeyup={onkeyup}
  >
    {#if title.id && title.title}
      <title id="{title.id}">{title.title}</title>
    {/if}
    {#if desc.id && desc.desc}
      <desc id="{desc.id}">{desc.desc}</desc>
    {/if}
      <path d="M32 32C32 14.3 46.3 0 64 0H256c17.7 0 32 14.3 32 32s-14.3 32-32 32H64C46.3 64 32 49.7 32 32zM0 160c0-35.3 28.7-64 64-64H256c35.3 0 64 28.7 64 64V448c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V160zm112 0H69.8c-3.2 0-5.8 2.6-5.8 5.8C64 198 90 224 122.2 224H144h32 21.8c32.1 0 58.2-26 58.2-58.2c0-3.2-2.6-5.8-5.8-5.8H208c-19.1 0-36.3 8.4-48 21.7c-11.7-13.3-28.9-21.7-48-21.7zm48 117.7c-11.7-13.3-28.9-21.7-48-21.7H69.8c-3.2 0-5.8 2.6-5.8 5.8C64 294 90 320 122.2 320H144h32 21.8c32.1 0 58.2-26 58.2-58.2c0-3.2-2.6-5.8-5.8-5.8H208c-19.1 0-36.3 8.4-48 21.7zM112 352H69.8c-3.2 0-5.8 2.6-5.8 5.8C64 390 90 416 122.2 416H144v32c0 8.8 7.2 16 16 16s16-7.2 16-16V416h21.8c32.1 0 58.2-26 58.2-58.2c0-3.2-2.6-5.8-5.8-5.8H208c-19.1 0-36.3 8.4-48 21.7c-11.7-13.3-28.9-21.7-48-21.7z"/>
  </svg>
{:else}
  <svg
    xmlns="http://www.w3.org/2000/svg"
    {...restProps}
    {role}
    width={size}
    height={size}
    class={classname}
    fill={color}
    aria-label={ariaLabel}
    aria-describedby={hasDescription ? ariaDescribedby : undefined}
    viewBox="0 0 320 512"
  >
    {#if title.id && title.title}
      <title id="{title.id}">{title.title}</title>
    {/if}
    {#if desc.id && desc.desc}
      <desc id="{desc.id}">{desc.desc}</desc>
    {/if}
      <path d="M32 32C32 14.3 46.3 0 64 0H256c17.7 0 32 14.3 32 32s-14.3 32-32 32H64C46.3 64 32 49.7 32 32zM0 160c0-35.3 28.7-64 64-64H256c35.3 0 64 28.7 64 64V448c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V160zm112 0H69.8c-3.2 0-5.8 2.6-5.8 5.8C64 198 90 224 122.2 224H144h32 21.8c32.1 0 58.2-26 58.2-58.2c0-3.2-2.6-5.8-5.8-5.8H208c-19.1 0-36.3 8.4-48 21.7c-11.7-13.3-28.9-21.7-48-21.7zm48 117.7c-11.7-13.3-28.9-21.7-48-21.7H69.8c-3.2 0-5.8 2.6-5.8 5.8C64 294 90 320 122.2 320H144h32 21.8c32.1 0 58.2-26 58.2-58.2c0-3.2-2.6-5.8-5.8-5.8H208c-19.1 0-36.3 8.4-48 21.7zM112 352H69.8c-3.2 0-5.8 2.6-5.8 5.8C64 390 90 416 122.2 416H144v32c0 8.8 7.2 16 16 16s16-7.2 16-16V416h21.8c32.1 0 58.2-26 58.2-58.2c0-3.2-2.6-5.8-5.8-5.8H208c-19.1 0-36.3 8.4-48 21.7c-11.7-13.3-28.9-21.7-48-21.7z"/>
  </svg>
{/if}

<!--
@component
[Go to docs](https://svelte-awesome-icons.codewithshin.com/)
## Props
@props: 
-->
