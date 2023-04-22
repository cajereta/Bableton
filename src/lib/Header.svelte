<script>
  import { Hamburger } from "svelte-hamburgers";
  const listRight = ["Live", "Push", "Note", "Link", "Shop", "Packs", "Help"];
  const listSecondary = ["Jobs", "Apprenticeships"];
  let y = window.scrollY;
  $: console.log(y);
  let prevScroll = window.pageYOffset;
  let open;
  import { fly } from "svelte/transition";
  let innerWidth;
</script>

<svelte:window
  bind:innerWidth
  bind:scrollY={y}
  on:scroll={() => {
    let currentScroll = window.pageYOffset;

    if (prevScroll > currentScroll) {
      document.getElementById("navbar").style.top = "0";
      document.getElementById("scroll").style.padding = "1rem 1.5rem 0.5rem ";
      document.getElementById("scroll").style.margin = "1rem 0rem 0.3rem ";
    } else {
      document.getElementById("navbar").style.top = "-50px";
      document.getElementById("scroll").style.padding = "0.5rem 1.5rem 0rem";
      document.getElementById("scroll").style.margin = "0.9rem 0rem 0.5rem ";
    }
    if (y < 85) {
      document.getElementById("scroll").style.padding = "0.5rem 1.5rem 0.2rem ";
      document.getElementById("scroll").style.margin = "0.9rem 0rem 0.5rem ";
    }
    prevScroll = currentScroll;
  }}
/>

<div class="header" id="navbar" class:sticky={y > 82}>
  <nav class=" primary" class:hide={y > 82}>
    <a href={"#"} class="logo">
      <svg
        role="img"
        aria-labelledby="logo"
        class="main-nav__logo__image"
        xmlns="http://www.w3.org/2000/svg"
        width="45"
        height="21"
        viewBox="0 0 45 21"
        ><title id="logo">Ableton Homepage</title><path
          d="M0 0h3v21H0zM6 0h3v21H6zM12 0h3v21h-3zM18 0h3v21h-3zM24 18h21v3H24zM24 12h21v3H24zM24 6h21v3H24zM24 0h21v3H24z"
        /></svg
      >
    </a>
    {#if innerWidth < 1024}
      <Hamburger
        bind:open
        --padding="20px 0px 22px 20px"
        --layer-spacing="6px"
      />
      {#if open}
        <div class="burger" />
      {/if}
    {:else}
      <ul>
        {#each listRight as item}
          <li><a href={"#"}>{item}</a></li>
        {/each}
        <li><a href={"#"} id="orange">More+</a></li>
        <li class="left tiny"><a href={"#"}>Try Live for free</a></li>
        <li class="tiny right"><a href={"#"}> Log in or register</a></li>
      </ul>
    {/if}
  </nav>

  <div class="separator" class:hide={y > 82} />
  <nav class="secondary" class:hide2={y > 82}>
    <ul class="bottom-nav" id="scroll">
      <li><a href={"#"} id="orange">About</a></li>
      {#each listSecondary as item}
        <li><a href={"#"}> {item}</a></li>
      {/each}
    </ul>
  </nav>
</div>

<style>
  .logo {
    margin-left: 1.5rem;
    padding-left: 1.5rem;
    scale: 1.3;
  }
  .header {
    background-color: #fff;
    width: 100%;
    padding: 10px 0;
    align-items: center;
    align-content: center;
  }
  nav {
    display: flex;
    align-items: center;
    justify-content: space-around;
    font-weight: bold;
  }
  ul {
    display: flex;
    width: 100%;
    gap: 15px;
    list-style: none;
    margin-right: 1rem;
    margin-bottom: 1.3rem;
  }

  a {
    color: #000;
    text-decoration: none;
  }

  .left {
    margin-left: auto;
  }
  .left a {
    color: #0000ff;
  }
  .separator {
    height: 0;
    display: block;
    border-top: 2px solid #eee;
  }
  #orange {
    color: #ff764d;
  }
  .primary {
    display: flex;
    align-items: center;
  }
  .bottom-nav {
    margin-bottom: 0.5rem;
    padding-left: 1.5rem;
    padding-top: 0.5rem;
  }
  .secondary {
    padding: 0 1.45rem;
    font-size: 0.9rem;
  }
  .hide2 {
    display: block;
  }

  @media (min-width: 80em) {
    .header {
      font-size: 1.1rem;
      line-height: 1.5;
      font-weight: bold;
    }
  }
  ul {
    align-items: center;
  }
  li {
    margin-right: 0.6rem;
    line-height: 1.5;
  }
  .right {
    font-size: 0.85rem;
  }

  .sticky {
    position: -webkit-sticky;
    position: sticky;
    z-index: 20;
    overflow: visible;
    top: 0;
    padding-top: 0;
    opacity: 80%;
  }
  .hide {
    display: none;
    transition: all ease;
  }
  @media (max-width: 64em) {
    nav.primary {
      justify-content: start;
      gap: 10px;
    }
    .burger {
      color: #000;
      text-align: center;
      font-size: 1.5em;
      letter-spacing: 0.15em;
      padding: 1em;
      padding-top: 0;
      z-index: 30;
      position: relative;
      margin-left: auto;
      display: flex;
      flex-direction: column;
    }
    .logo {
      margin-left: 0.9rem;
      padding-left: 1.5rem;
      scale: 1.3;
    }
  }
</style>
