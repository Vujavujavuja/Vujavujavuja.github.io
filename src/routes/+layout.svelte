<script>
    import '../app.css';
    import { onMount, onDestroy } from 'svelte';
    import Navbar from '../lib/Navbar.svelte';
  
    let vantaEffectContainer; // Reference for the Vanta effect container
  
    let vantaEffect;
  
    onMount(() => {
      const setVanta = () => {
        if (window.VANTA) {
          vantaEffect = window.VANTA.NET({
            el: vantaEffectContainer,
            mouseControls: true,
            touchControls: true,
            gyroControls: false,
            minHeight: 100.00,
            minWidth: 200.00,
            scale: 1.00,
            scaleMobile: 1.00,
            backgroundColor: 0x101010,
            points: 6.00,
            maxDistance: 23.00,
            spacing: 20.00,
          });
        }
      };
  
      setVanta();
  
      return () => {
        if (vantaEffect) vantaEffect.destroy();
      };
    });
  
    onDestroy(() => {
      if (vantaEffect) vantaEffect.destroy();
    });
  </script>
  
  <svelte:head>
    <title>Nemanja Vujic</title>
  </svelte:head>
  
  <div class="flex flex-col h-screen overflow-hidden">
    <Navbar class="z-20" />
    <div bind:this={vantaEffectContainer} class="flex-grow relative">
      <div class="overlay bg-zinc-900 opacity-60 absolute top-0 left-0 w-full h-full"></div>
      <main class="flex-1 overflow-auto z-10 relative">
          <slot></slot>
      </main>
    </div>
  </div>
  
  <style>
    .overlay {
      pointer-events: none;
    }
  </style>
  