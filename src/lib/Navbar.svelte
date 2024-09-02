<script>
    import { browser } from '$app/environment';
    import { onMount, onDestroy } from 'svelte';
    import 'animate.css';
    let showDropdown = false;
    let isMobile = false;

    if (browser) {
        const updateScreen = () => {
            isMobile = window.innerWidth < 768;
        };

        onMount(() => {
            window.addEventListener('resize', updateScreen);
            updateScreen(); // Initial check
        });

        onDestroy(() => {
            window.removeEventListener('resize', updateScreen);
        });
    }

    function toggleDropdown() {
        showDropdown = !showDropdown;
    }

    let animateClass = '';

    function applyAnimation() {
        animateClass = 'animate__animated animate__rubberBand';
    }

    function removeAnimation() {
        animateClass = '';
    }
</script>

<style>
    
    .nav-link {
        @apply transition-all duration-300 ease-in-out text-white;
        /* Custom hover effects from the original CSS */
        position: relative;
        overflow: hidden;
    }
    .nav-link:hover {
        @apply scale-105; /* Tailwind does not support scale(2), so we approximate */
        color: #000000; /* Preserved from the original */
    }
    .nav-link:hover::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: #ff497c;
        transition: transform 0.5s;
        transform-origin: left;
        transform: scaleX(1);
        z-index: -1;
    }
    .nav-link::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: #ff497c;
        transition: transform 0.5s;
        transform-origin: right;
        transform: scaleX(0);
        z-index: -1;
    }

    .dropdown-enter {
        transform: translateY(-10px);
        opacity: 0;
    }
    .dropdown-enter-active {
        transform: translateY(0);
        opacity: 1;
        transition: opacity 0.3s ease, transform 0.3s ease;
    }
    .logoN {
        @apply w-12 h-12;
    }
    .logoN:hover {
        @apply animate-spin;
    }
</style>

<nav class="bg-black text-white p-6 font-mono relative shadow-md shadow-zinc-900" style="z-index: 20;">
    <div class="container mx-auto flex justify-between items-center">
        <a href="/" class="flex items-center">
            <img src="/src/images/logoN.png" alt="logoN" class="logoN w-12 h-12">
        </a>
        {#if isMobile}
            <button on:click={toggleDropdown} class="text-xl">
                {#if showDropdown}X{:else}☰{/if}
            </button>
            {#if showDropdown}
                <div class="dropdown-enter {showDropdown ? 'dropdown-enter-active' : ''} absolute top-full right-0 bg-black w-full flex flex-col items-center z-10">
                    <a href="/about" class="text-xl p-2">About me</a>
                    <a href="/skills" class="text-xl p-2">Skills</a>
                    <a href="/projects" class="text-xl p-2">Projects</a>
                    <a href="/contact" class="text-xl p-2">Contact</a>
                </div>
            {/if}
        {:else}
            <div class="flex justify-between space-x-20">
                <a href="/about" class="mx-6 text-xl nav-link">About me</a>
                <a href="/skills" class="mx-6 text-xl nav-link">Skills</a>
                <a href="/projects" class="mx-6 text-xl nav-link">Projects</a>
                <a href="/contact" class="mx-6 text-xl nav-link">Contact</a>
            </div>
        {/if}
    </div>
</nav>
