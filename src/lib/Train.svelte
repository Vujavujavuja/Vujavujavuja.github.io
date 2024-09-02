<script>
    import { onMount } from 'svelte';

    let key = 0; // A key to force re-render

    // Function to reset animation
    function resetAnimation() {
        key++; // Increment key to force re-render and restart animation
    }
</script>

<style>
    @keyframes slideRight {
        from {
            transform: translateX(-300vw);
        }
        to {
            transform: translateX(100vw);
        }
    }

    .animated-box {
        animation: slideRight 10s linear infinite;
        background-color: blue; 
        width: 100px;
        height: 100px;
    }
</style>

<!-- Box with animation -->
<div key={key} class="animated-box" on:animationiteration={resetAnimation}></div>
