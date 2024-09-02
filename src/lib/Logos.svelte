<script>
    const numBoxes = 10;
    let boxes = [];
    
    const imageUrls = [
        '../src/images/javaLogo.png',
        '../src/images/cLogo.png',
        '../src/images/pythonLogo.png',
        '../src/images/jsLogo.png',
        '../src/images/rubyLogo.png',
        '../src/images/svelteLogo.png',
        '../src/images/cppLogo.png',
        '../src/images/sqlLogo.png',
        '../src/images/gitLogo.png',
        '../src/images/vueLogo.png'
    ];
    
    // Configurable positions
    let startY = -5;
    let endY = 100;
    let startX = 0;
    let maxX = 0;
    
    for (let i = 0; i < numBoxes; i++) {
        boxes.push({
            id: i,
            x: i,
            size: 5,
            duration: Math.random() * 5 + 5,
            imageUrl: imageUrls[i]
        });
    }
</script>
    
    
    
<style>
.box {
    position: relative;
    animation-name: fly;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
    background-size: cover;
}

@keyframes fly {
    0% {
        transform: translateY(var(--startY));
    }
    100% {
        transform: translateY(var(--endY));
    }
}
</style>
    
{#each boxes as { id, x, size, duration, imageUrl }}
<div
    class="box"
    style="left:{x}vw; width:{size + 1}vh; height:{size + 1}vh; animation-duration: {duration}s; --startY:{startY}vh; --endY:{endY}vh; background-image: url({imageUrl});"
/>
{/each}
