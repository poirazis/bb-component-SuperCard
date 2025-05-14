<script>
  import { getContext } from "svelte";
  import SuperButton from "../../bb_super_components_shared/src/lib/SuperButton/SuperButton.svelte";
  import SuperPopover from "./../../bb_super_components_shared/src/lib/SuperPopover/SuperPopover.svelte";
  import { get } from "svelte/store";

  export let title;
  export let subtitle;
  export let text;

  export let showImage;
  export let imageUrl;
  export let padded;

  export let buttons;
  export let collapsed = false;
  export let menuIcon = "ri-more-2-fill";
  export let showFooter;
  export let footer;
  export let footerButtons;
  export let cardType;

  export let flex;

  let anchor;
  let open = false;
  let align = "flex-end";

  const { styleable, enrichButtonActions } = getContext("sdk");
  const component = getContext("component");
  const context = getContext("context");

  $: $component.styles = {
    ...$component.styles,
    normal: {
      background: "var(--spectrum-global-color-gray-50)",
      border: "1px solid var(--spectrum-global-color-gray-300)",
      flex: flex ? "1 0 auto" : "none",
      width: cardType == "vertical" ? "19rem" : "26rem",
      ...$component.styles.normal,
    },
  };

  $: withSlot = $component.children;
</script>

<div class="super-card-outer" use:styleable={$component.styles}>
  <div
    class="super-card"
    class:withSlot
    class:withFooter={showFooter}
    class:vertical={cardType == "vertical"}
    class:with-background={cardType == "image"}
    class:padded
    style:--contents-opacity={open ? 0.9 : 0}
  >
    <div
      class="super-card-body"
      class:padded
      class:with-background={cardType == "image"}
      style="background-image: url({cardType == 'image' ? imageUrl : null});"
    >
      <div class="super-card-header">
        {#if showImage && imageUrl && cardType != "image"}
          <div
            class="super-card-header-image-container"
            class:vertical={cardType == "vertical"}
            class:padded
          >
            <div
              class="super-card-header-image"
              style="background-image: url({imageUrl});"
            ></div>
          </div>
        {/if}

        <div
          class="super-card-header-contents"
          class:vertical={cardType == "vertical"}
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

          {#if text}
            <div class="super-card-main-text">{text}</div>
          {/if}

          {#if !collapsed && buttons?.length}
            <div class="super-card-buttons">
              {#each buttons as button}
                <SuperButton
                  {...button}
                  onClick={enrichButtonActions(button?.onClick, $context)}
                />
              {/each}
            </div>
          {/if}
        </div>
      </div>
    </div>

    {#if $component?.children}
      <div class="super-card-slot-content">
        <slot />
      </div>
    {/if}

    {#if showFooter}
      <div
        class="super-card-footer"
        class:with-background={cardType == "image"}
      >
        <span> {footer || ""}</span>
        <div class="super-card-footer-buttons">
          {#if footerButtons?.length}
            {#each footerButtons as button}
              <SuperButton
                {...button}
                size="S"
                quiet
                type="secondary"
                onClick={enrichButtonActions(button?.onClick, $context)}
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
              {...button}
              menuItem
              menuAlign={align == "flex-start" ? "left" : "right"}
              iconAfterText={align != "flex-start"}
              onClick={enrichButtonActions(button?.onClick, $context)}
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
    flex-direction: column;
    align-items: stretch;
    overflow: hidden;
    min-height: 8rem;
  }
  .super-card {
    flex: auto;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    gap: 1rem;

    &.vertical {
      max-height: unset;
      padding-bottom: 1rem;
      & *.super-card-header {
        flex-direction: column;
        overflow: hidden;
      }
    }

    &.padded {
      padding: 1rem;

      & *.super-card-header {
        gap: 1rem;
        padding: 0rem;
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

    &.with-background {
      gap: 0rem;
    }
  }

  .super-card-body {
    flex: auto;
    flex-direction: column;
    align-items: stretch;
    background-size: cover;
    background-position: center;
    transition: all 230ms ease-in-out;
    padding: 0rem;
    display: flex;
    align-items: flex-start;

    &.padded {
      padding: 0rem;
    }
    &.with-background {
      padding: 1.25rem;
      justify-content: flex-end;
      &:hover {
        --contents-opacity: 0.85;
      }
    }
  }

  .super-card-header {
    width: 100%;
    display: flex;
    align-items: stretch;
    overflow: hidden;
    gap: 1rem;
  }

  .super-card-header-image-container {
    flex: 1 0 auto;
    display: flex;
    align-items: stretch;
    justify-content: stretch;
    min-width: 6rem;
    overflow: hidden;
    max-width: 6rem;
    min-height: 6rem;

    &.small {
      min-width: 6rem;
      min-height: 100%;
    }

    &.vertical {
      max-width: unset;
      width: 100%;
      min-height: 8rem;
    }

    &.padded {
      border-radius: 0.25rem;
    }
  }
  .super-card-header-image {
    flex: 1 0 auto;
    background-size: cover;
    background-position: center;
    transition: all 230ms ease-in-out;

    &:hover {
      transform: scale(1.1);
    }
  }

  .super-card-header-contents {
    flex: auto;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 1rem;
    padding-left: 0rem;
    overflow: hidden;
    gap: 1rem;

    &.over-background {
      background-color: var(--spectrum-global-color-gray-50);
      border-radius: 0.5rem;
      opacity: var(--contents-opacity, 0);
      transition: all 230ms;
      padding: 1rem;
    }

    &.vertical {
      padding: 0rem 1rem;
      gap: 1.5rem;
    }

    &.padded:not(.over-background) {
      padding: 0rem;
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
    font-weight: 600;
    color: var(--spectrum-global-color-gray-800);
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
    font-size: 16px;
  }

  .super-card-subtitle {
    height: 1.25rem;
    font-size: var(--super-card-subtitle-font-size, 13px);
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
    align-items: center;
    gap: var(--super-card-buttons-gap, 8px);
    width: 100%;
  }
  .super-card-footer-buttons {
    display: flex;
    align-items: center;
    gap: var(--super-card-buttons-gap, 8px);
  }

  .super-card-slot-content {
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
    height: 2.4rem;
    transition: all 230ms ease-in-out;

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
    opacity: 0.9;
  }
</style>
