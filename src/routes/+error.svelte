<script>
    
    let goBack = () => {
        window.history.back();
    };

    export let error = {
        status: 404,
        message: "Oh no! It looks like this page doesn't exist.",
    };
</script>

<main>
  <h1 class="font-mono text-pink-500">{error.status}</h1>
  <p class="pb-10 font-mono text-pink-500">{error.message}</p>
  <button class="btn text-black font-mono font-bold text-2xl bg-pink-500 p-2" on:click={goBack}>Go back</button>
</main>

<style>
    * {
        overflow: hidden;
    }
    main {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
        text-align: center;
    }

    h1 {
        font-size: 4rem;
        margin-bottom: 1rem;
    }

    p {
        font-size: 1.5rem;
    }
    .btn {
            @apply transition-all duration-300 ease-in-out;
            @apply rounded-lg;
            animation: glow 0.99999s infinite alternate;
            
        }
        .btn:hover {
            @apply bg-pink-500 hover:bg-black text-black hover:text-pink-500;
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
