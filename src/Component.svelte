<script>
  import { getContext } from "svelte";
  import SuperButton from "../../bb_super_components_shared/src/lib/SuperButton/SuperButton.svelte";
  import SuperPopover from "./../../bb_super_components_shared/src/lib/SuperPopover/SuperPopover.svelte";

  export let title = "Super Card";
  export let subtitle = "Subtitle";
  export let text = "This is a super card";
  export let footer = "Footer";
  export let showImage;
  export let imageUrl = "https://picsum.photos/seed/picsum/200/300";
  export let padded;

  export let buttons;
  export let collapsed = false;
  export let menuIcon = "ri-more-2-fill";
  export let footerButtons;
  export let cardType;

  export let flex;

  let anchor;
  let open = false;
  let align = "flex-end";
  let buttonClass;
  let quiet = false;
  let iconOnly = false;

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  $: $component.styles = {
    ...$component.styles,
    normal: {
      background: "var(--spectrum-global-color-gray-50)",
      border: "1px solid var(--spectrum-global-color-gray-300)",
      flex: flex ? "1 0 auto" : "none",
      width: flex ? "100%" : "360",
      ...$component.styles.normal,
    },
  };

  $: withSlot = $component.children;
  $: effectivePadded = padded && cardType != "image";
</script>

<div class="super-card-outer" use:styleable={$component.styles}>
  <div
    class="super-card"
    class:withSlot
    class:withFooter={footer}
    class:square={cardType == "square"}
    class:vertical={cardType == "vertical"}
    class:padded={effectivePadded}
  >
    <div
      class="super-card-body"
      class:with-background={cardType == "image"}
      style="background-image: url({cardType == 'image' ? imageUrl : null});"
    >
      <div class="super-card-header">
        {#if showImage && imageUrl && cardType != "image"}
          <div
            class="super-card-header-image-container"
            class:vertical={cardType == "vertical"}
          >
            <div
              class="super-card-header-image"
              style="background-image: url({imageUrl});"
            ></div>
          </div>
        {/if}

        <div
          class="super-card-header-contents"
          class:padded
          class:over-background={cardType == "image"}
        >
          <div class="super-card-header-text">
            <div class="super-card-header-title">
              <div class="super-card-title">{title}</div>
              {#if collapsed && buttons?.length}
                <!-- svelte-ignore a11y-click-events-have-key-events -->
                <!-- svelte-ignore a11y-no-static-element-interactions -->
                <i
                  bind:this={anchor}
                  class={menuIcon ?? "ri-more-2-fill"}
                  class:menu-icon={true}
                  class:open
                  on:click={() => (open = !open)}
                ></i>
              {/if}
            </div>
            <div class="super-card-subtitle">{subtitle}</div>
          </div>
          {#if (!buttons?.length || (buttons?.length && collapsed)) && text}
            <div class="super-card-main-text">{text}</div>
          {/if}
          {#if !collapsed && buttons?.length}
            <div class="super-card-buttons">
              {#each buttons as button}
                <SuperButton
                  {...button}
                  on:click={() => {
                    button.action();
                  }}
                />
              {/each}
            </div>
          {/if}
        </div>
      </div>

      {#if $component?.children}
        <div class="super-card-slot-content">
          <slot />
        </div>
      {/if}
    </div>

    {#if footer || footerButtons?.length}
      <div
        class="super-card-footer"
        class:with-background={cardType == "image"}
      >
        {footer}
        <div class="super-card-buttons">
          {#if footerButtons?.length}
            {#each footerButtons as button}
              <SuperButton
                {...button}
                on:click={() => {
                  button.action();
                }}
              />
            {/each}
          {/if}
        </div>
      </div>
    {/if}
  </div>

  {#if open}
    <SuperPopover {anchor} {open} on:close={() => (open = false)}>
      <!-- svelte-ignore a11y-no-static-element-interactions -->
      <div class="button-list">
        {#if buttons?.length}
          {#each buttons as button}
            <SuperButton
              {buttonClass}
              {quiet}
              {iconOnly}
              {...button}
              menuItem
              menuAlign={align == "flex-start" ? "left" : "right"}
              iconAfterText={align != "flex-start"}
              on:click={() => (open = false)}
            />
          {/each}
        {/if}
      </div>
    </SuperPopover>
  {/if}
</div>

<style>
  .super-card-outer {
    display: flex;
    align-items: stretch;
  }
  .super-card {
    flex: auto;
    border-radius: 0.25rem;
    display: flex;
    flex-direction: column;
    align-items: stretch;

    &.square {
      aspect-ratio: 1;
      justify-content: space-between;
    }

    &.vertical {
      max-height: unset;
      & *.super-card-header {
        flex-direction: column;
        overflow: hidden;
      }
    }

    &.padded {
      padding: 1rem;

      & *.super-card-header-contents {
        padding: 0rem;
      }

      & *.super-card-header {
        gap: 1rem;
      }

      & *.super-card-slot-content {
        padding: 0rem;
      }

      & *.super-card-footer {
        padding: 0rem;
      }
    }

    &.withSlot:not(.withFooter) {
      max-height: unset !important;
      padding-bottom: 1rem;
    }

    &.withFooter {
      padding-bottom: 0rem;
    }
  }

  .super-card-header {
    flex: auto;
    display: flex;
    align-items: stretch;
    overflow: hidden;
  }

  .super-card-header-image-container {
    flex: 1 0 auto;
    display: flex;
    align-items: stretch;
    justify-content: stretch;
    min-width: 6rem;
    overflow: hidden;
    max-width: 6rem;

    &.small {
      min-width: 6rem;
      min-height: 100%;
    }

    &.vertical {
      max-width: unset;
      width: 100%;
      min-height: 6rem;
    }
  }
  .super-card-header-image {
    flex: 1 0 auto;
    background-size: cover;
    background-position: center;
    border-radius: var(--super-card-image-border-radius, 0.25rem);
    transition: all 230ms ease-in-out;

    &:hover {
      transform: scale(1.1);
    }
  }

  .super-card-body {
    flex: auto;
    background-size: cover;
    background-position: center;
    transition: all 230ms ease-in-out;
    padding: 0rem;

    &:hover {
      filter: grayscale();
      --contents-opacity: 0.9;
    }

    &.with-background {
      padding: 1.25rem;
    }
  }

  .super-card-header-contents {
    flex: auto;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 1rem;
    overflow: hidden;
    gap: 1rem;

    &.over-background {
      background-color: var(--spectrum-global-color-gray-50);
      border-radius: 0.5rem;
      opacity: var(--contents-opacity, 0);
      transition: all 230ms;

      &:hover {
        backdrop-filter: blur(10);
      }
    }
  }

  .super-card-header-title {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
    width: 100%;
    overflow: hidden;
  }

  .super-card-header-text {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: space-between;
    min-width: 0;
    overflow: hidden;
  }

  .super-card-title {
    font-weight: 700;
    color: var(--spectrum-global-color-gray-900);
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
  }

  .super-card-subtitle {
    height: 1rem;
    font-size: var(--super-card-subtitle-font-size, 12px);
    color: var(--spectrum-global-color-gray-700);
    text-transform: uppercase;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
    width: 100%; /* Ensure full width for ellipsis */
  }

  .super-card-main-text {
    font-size: var(--super-card-text-font-size, 15px);
    color: var(--spectrum-global-color-gray-700);
    overflow: hidden;
    white-space: normal; /* Allow multiline wrapping */
    display: -webkit-box;
    -webkit-line-clamp: 2; /* Limit to 3 lines */
    -webkit-box-orient: vertical;
    width: 100%;
    height: 2.5rem; /* Approx 3 lines at 15px font */
  }

  .super-card-buttons {
    display: flex;
    gap: var(--super-card-buttons-gap, 8px);
  }

  .super-card-slot-content {
    margin-top: 1rem;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    padding: 0rem 1rem;
  }

  .super-card-footer {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: var(--super-card-footer-font-size, 12px);
    color: var(--spectrum-global-color-gray-600);
    border-top: 1px solid var(--spectrum-global-color-gray-200);
    padding: 0rem 1rem;
    line-height: 2.4rem;
    transition: all 230ms ease-in-out;
    margin-top: 8px;

    &:hover {
      color: var(--spectrum-global-color-gray-700);
    }

    &.with-background {
      margin-top: 0px;
    }
  }

  .menu-icon {
    &:hover {
      cursor: pointer;
      color: var(--spectrum-global-color-gray-900);
    }

    &.open {
      color: var(--spectrum-global-color-gray-900);
      font-weight: 800;
    }
  }

  .button-list {
    display: flex;
    flex-direction: column;
    align-items: stretch;
    min-width: 120px;
    background-color: var(--spectrum-global-color-gray-50);
  }
</style>
