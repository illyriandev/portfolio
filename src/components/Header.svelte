<script>
  import { onMount } from "svelte";

  let width;
  let showMenu = false;
  let activePage;
  export let color;

  onMount(() => {
    document.querySelector(".scroll").scroll(0, 0);
  });
</script>

<svelte:window bind:innerWidth={width} />

<header
  style="{showMenu
    ? 'height: 100%; background-color: #161411;'
    : 'background-color: linear-gradient(rgba(0, 0, 0, 1) 40%, rgba(0, 0, 0, 0) 100%); '}
        --color: {color};"
>
  <!-- <div class="title"> -->
  {#if width > 767}
    <h1><a href="./">ILLYRIAN</a></h1>
    <nav>
      <a class={activePage == "development" ? "bolder" : ""} href="/development"
        >DEV</a
      >
      <a class={activePage == "video" ? "bolder" : ""} href="/video">VIDEO</a>
      <a class={activePage == "design" ? "bolder" : ""} href="/design">DESIGN</a
      >
    </nav>
    <div class="static-nav">
      <a href="./#about-card">ABOUT</a>
      <a href="#contact-card">CONTACT</a>
    </div>
  {:else}
    <div class="title flex w-full">
      <h1><a href="/">ILLYRIAN</a></h1>
      <button
        on:click={() => {
          showMenu = !showMenu;
        }}
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 448 512"
          style="fill: {color};"
          ><!--! Font Awesome Free 6.4.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. --><path
            d="M0 96C0 78.3 14.3 64 32 64H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H32C14.3 128 0 113.7 0 96zM0 256c0-17.7 14.3-32 32-32H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H32c-17.7 0-32-14.3-32-32zM448 416c0 17.7-14.3 32-32 32H32c-17.7 0-32-14.3-32-32s14.3-32 32-32H416c17.7 0 32 14.3 32 32z"
          /></svg
        >
      </button>
    </div>
    {#if showMenu}
      <div class="nav">
        <nav class="w-full flex justify-center gap-8">
          <a
            class={activePage == "development" ? "bolder" : ""}
            href="/development">DEV</a
          >
          <a class={activePage == "video" ? "bolder" : ""} href="/video"
            >VIDEO</a
          >
          <a class={activePage == "design" ? "bolder" : ""} href="/design"
            >DESIGN</a
          >
        </nav>
        <div class="static-nav w-full flex justify-center gap-8">
          <a
            on:click={() => {
              showMenu = false;
            }}
            href="#about-card">ABOUT</a
          >
          <a
            on:click={() => {
              showMenu = false;
            }}
            href="#contact-card">CONTACT</a
          >
        </div>
      </div>
    {/if}
  {/if}
  <!-- </div> -->
  <div class="blur" style={showMenu ? "backdrop-filter: blur(40px);" : ""} />
</header>

<style lang="postcss">
  header {
    height: 60px;
    width: 100%;

    margin: auto;
    padding: 1rem 5% 1rem 5%;

    position: absolute;
    z-index: 100;
    overflow: hidden;

    display: flex;
    justify-content: space-between;
    align-items: center;

    color: var(--color);

    transition: 0.4s all ease-in-out;

    @media (min-width: 1440px) {
      height: 80px;
    }

    @media (max-width: 767px) {
      flex-direction: column;
      gap: 2rem;

      .title {
        justify-content: space-between;
      }

      .nav {
        height: 90%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        gap: 6rem;

        & > nav,
        & > .static-nav {
          flex-direction: column;
          align-items: center;

          a {
            font-size: 2.5rem;
          }
        }
      }
    }

    .title,
    .nav {
      z-index: 100;
    }

    .blur {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      backdrop-filter: blur(70px);
      z-index: 1;
    }

    h1 {
      font-family: "Righteous", sans-serif;
      font-size: 2rem;
      font-weight: 400;
      z-index: 200;
    }

    button {
      z-index: 200;
      svg {
        height: 25px;
        width: auto;
        fill: #fff;
      }
    }

    nav,
    .static-nav {
      display: flex;
      gap: 1.5rem;
      z-index: 200;

      a {
        font-size: 1.25rem;
        font-weight: 300;
        transition: 0.25s all ease-in;

        &:hover {
          color: var(--primary);
          background-color: #fff;
        }
      }
    }
  }
</style>
