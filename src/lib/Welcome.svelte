<script>
    import Typewriter from 'svelte-typewriter';
    import { concurrent } from 'svelte-typewriter';
    import { browser } from '$app/environment';
    import { onMount, onDestroy } from 'svelte';
    let isMobile = false;

    let getInContact = () => {
        window.location.href = '/contact';
    };

    let getInProject = () => {
        window.location.href = '/projects';
    };

    if (browser) {
        const updateScreen = () => {
            isMobile = window.innerWidth < 768;
        };

        onMount(() => {
            window.addEventListener('resize', updateScreen);
            updateScreen(); 
        });

        onDestroy(() => {
            window.removeEventListener('resize', updateScreen);
        });
    }
</script>

<style>
    .typewriter-containerh1e {
        min-height: 50px;
    }
    .typewriter-containere{
        min-height: 175px;
    }
    .typewriter-containerh1 {
        min-height: 50px;
    }
    .typewriter-container{
        min-height: 350px;
    }
    .hover-grow {
        /* Apply transition properties to the default state */
        @apply transition-all duration-300 ease-in-out;
    }
    .hover-grow:hover {
        @apply text-pink-500 hover:text-pink-500 text-lg hover:text-3xl;
    }
    .btn {
        @apply transition-all duration-300 ease-in-out;
        @apply rounded-lg;
        animation: glow 0.99999s infinite alternate;
        
    }
    .btn:hover {
        @apply bg-pink-500 hover:bg-black text-black hover:text-pink-500;
    }
    .iframePC {
        position: fixed;
        bottom: 0;
        right: 0;
    }
    @keyframes glow {
            from {
        box-shadow: 0 0 5px -20px #E91E63;
        }
        to {
            box-shadow: 0 0 10px 0px #E91E63;
        }
}
</style>
{#if isMobile}
    <div class="w-full p-8 ">
        <h1 class="text-white font-mono text-2xl typewriter-containerh1">
            <Typewriter>
                <a href="/about" class={`hover-grow text-initial`}>Hello, I am Nemanja Vujić.</a>
            </Typewriter>
        </h1>
        <p use:concurrent={{interval: 10}} class="text-white font-mono text-xl pt-7 typewriter-container">
            Welcome to my professional portfolio. Currently, I am advancing my studies at Računarski fakultet, Belgrade, Serbia, where I am honing my skills in computer science. This website serves as a curated showcase of my projects, technical skills, and achievements. I invite you to explore my work and gain insights into my professional journey and capabilities.
        </p>
        <div class="pt-7 flex space-x-20">
            <button class="btn text-black font-mono font-bold text-lg bg-pink-500 p-2" on:click={getInContact}>Get in contact</button>
            <button class="btn text-black font-mono font-bold text-lg bg-pink-500 p-2" on:click={blogBlog}>Checkout my blog</button>
        </div>
    </div>
{:else}
    <div class="w-full p-8 ">
        <h1 class="text-white font-mono text-2xl typewriter-containerh1e">
            <Typewriter>
                <a href="/about" class={`hover-grow text-initial`}>Hello, I am Nemanja Vujić.</a>
            </Typewriter>
        </h1>
        <p use:concurrent={{interval: 30}} class="text-white font-mono text-xl pt-7 typewriter-containere">
            
            Welcome to my professional portfolio. Currently, I am advancing my studies at Računarski fakultet, Belgrade, Serbia, where I am honing my skills in computer science. This website serves as a curated showcase of my projects and technical skills. I invite you to explore my work and gain insights into my professional journey and capabilities.
        </p>
        <div class="pt-7 flex space-x-20">
            <button class="btn text-black font-mono font-bold text-lg bg-pink-500 p-2" on:click={getInContact}>Get in contact</button>
            <button class="btn text-black font-mono font-bold text-lg bg-pink-500 p-2" on:click={getInProject}>Checkout my projects</button>
        </div>
        <iframe title="frame" src="https://lottie.host/embed/4352d048-23e3-4d0f-98cb-44dc2cec34a9/lPZtqRC3Cx.json" class="absolute bottom-0 right-0 w-[60vw] h-[60vh] iframePC"></iframe>
    </div>
{/if}
