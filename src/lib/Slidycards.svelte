<script>
    import { onMount } from 'svelte';
  
    let currentSlide = 0;
    let slides = [
      { heading: 'Slide 1', text: 'This is the first slide.' },
      { heading: 'Slide 2', text: 'This is the second slide.' },
      { heading: 'Slide 3', text: 'This is the third slide.' },
    ];
  
    function goToSlide(index) {
      currentSlide = index;
    }
  
    function nextSlide() {
      currentSlide = (currentSlide + 1) % slides.length;
    }
  
    function prevSlide() {
      currentSlide = (currentSlide + slides.length - 1) % slides.length;
    }
  
    // Auto-play the carousel
    let interval;
    onMount(() => {
      interval = setInterval(nextSlide, 3000);
      return () => clearInterval(interval);
    });
  </script>
  
  <style>
    .carousel {
      position: relative;
      overflow: hidden;
      max-width: 800px;
      margin: auto;
    }
  
    .carousel-inner {
      display: flex;
      transition: transform 0.5s ease;
    }
  
    .carousel-item {
      flex: 0 0 100%;
      text-align: center;
      background-color: #333;
      color: white;
      padding: 40px 20px;
      border-radius: 10px;
      margin: auto;
    }
  
    .controls {
      display: flex;
      justify-content: center;
      gap: 10px;
      margin-top: 20px;
    }
  
    .control {
      cursor: pointer;
      width: 30px;
      height: 30px;
      background-color: #ddd;
      border-radius: 2px;
      transition: background-color 0.3s ease, transform 0.3s ease;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 0.8em;
    }
  
    .control.active,
    .control:hover {
      background-color: #333;
      color: white;
      transform: scale(1.1);
    }
  
    h2 {
      margin: 0 0 10px;
      font-size: 1.8em;
    }
  
    p {
      margin: 0;
      font-size: 1.2em;
    }
  </style>
  
  <div class="carousel">
    <div class="carousel-inner" style="transform: translateX(-{currentSlide * 100}%);">
      {#each slides as slide}
        <div class="carousel-item">
          <h2>{slide.heading}</h2>
          <p>{slide.text}</p>
        </div>
      {/each}
    </div>
  
    <div class="controls">
      {#each slides as _, index}
        <div class="control {index === currentSlide ? 'active' : ''}" on:click={() => goToSlide(index)}>
          {index + 1}
        </div>
      {/each}
    </div>
  </div>
  