<script>
    import { browser } from '$app/environment';
    import { onMount, onDestroy } from 'svelte';
    import { slide, fade } from 'svelte/transition';

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

    // data
    let skills = [
        { name: 'Communication', level: 75, color: 'bg-blue-500', label: '75%', expanded: false },
        { name: 'Teamwork', level: 60, color: 'bg-green-500', label: '60%', expanded: false },
        { name: 'Problem Solving', level: 85, color: 'bg-yellow-500', label: '85%', expanded: false },
    ];

    let tools = [
        { name: 'VS Code', level: 70, color: 'bg-blue-500', label: '3 years' },
        { name: 'Git', level: 80, color: 'bg-red-500', label: '3.5 years' },
        {name: 'JetBrains IDE Family', level: 90, color: 'bg-fuchsia-500', label: '4 years'},
        {name: 'Visual Studio', level: 55, color: 'bg-purple-500', label: '1.5 years'},
        {name: 'Eclipse', level: 70, color: 'bg-indigo-500', label: '3 years'},
        {name: 'Code::Blocks', level: 90, color: 'bg-green-500', label: '4 years'},
    ];

    let languages = [
        { name: 'JavaScript', level: 85, color: 'bg-yellow-500', label: '85%' },
        { name: 'Python', level: 90, color: 'bg-blue-600', label: '90%' },
    ];

    let expandedState = {
        skills: false,
        tools: false,
        languages: false,
    };

    function toggleExpanded(category) {
        expandedState[category] = !expandedState[category];
    }

    function getSlideParams(category) {
        return expandedState[category] ? { duration: 300, y: -100 } : { duration: 300, y: 0 };
    }
</script>

<div class="{isMobile ? 'flex flex-col items-center space-y-4' : 'grid grid-cols-3 gap-8'}">
    <!-- Skills Card Example -->
    <div class="card shadow-lg rounded-lg p-4 bg-zinc-800 text-white transition duration-300 ease-in-out transform hover:scale-105 hover:shadow-2xl font-mono">
        <div class="flex justify-center mt-2">
            <h2 class="text-xl font-semibold mb-4">Skills</h2>
        </div>
        {#if expandedState.skills}
            <div class="mt-2 overflow-auto w-60 justify-normal" in:slide={getSlideParams('skills')} out:slide={getSlideParams('skills')}>
                <h1>Communication:</h1>
                <p>Communication is a skill that displays my communication skills</p>
                <h1>Teamwork:</h1>
                <p>Teamwork is a skill that displays my teamwork skills</p>
                <h1>Problem Solving:</h1>
                <p>Problem Solving is a skill that displays my problem solving skills</p>
                <!-- Display bars below all text -->
                {#each skills as skill}
                    <div class="mb-4">
                        <div class="text-sm font-medium mb-1">{skill.name}</div>
                        <div class="w-full bg-gray-700 rounded-full h-3">
                            <div class={skill.color + " h-3 rounded-full flex justify-end items-center pr-2"} style="width: {skill.level}%">
                                <span class="text-xs font-semibold text-white">{skill.label}</span>
                            </div>
                        </div>
                    </div>
                {/each}
            </div>
        {:else}
            {#each skills as skill (skill.name)}
                <div class="mb-4" in:fade={{ duration: 300 }}>
                    <div class="text-sm font-medium mb-1">{skill.name}</div>
                    <div class="w-full bg-gray-700 rounded-full h-3">
                        <div class={skill.color + " h-3 rounded-full flex justify-end items-center pr-2"} style="width: {skill.level}%">
                            <span class="text-xs font-semibold text-white">{skill.label}</span>
                        </div>
                    </div>
                </div>
            {/each}
        {/if}
        <div class="flex justify-center mt-4">
            <button class="btn" on:click={() => toggleExpanded('skills')}>
                {expandedState.skills ? 'Show less ⮝' : 'Show more ⮟'}
            </button>
        </div>
    </div>

    <!-- Tools Card -->
    <div class="card shadow-lg rounded-lg p-4 bg-zinc-800 text-white transition duration-300 ease-in-out transform hover:scale-105 hover:shadow-2xl font-mono">
        <div class="flex justify-center mt-2">
            <h2 class="text-xl font-semibold mb-4">Tools</h2>
        </div>
        {#if expandedState.tools}
            <div class="mt-2 overflow-auto w-60 justify-normal" in:slide={getSlideParams('tools')} out:slide={getSlideParams('tools')}>
                <!-- Display this simple text when expandedState.tools is true -->
                Comprehensive Tools Proficiency
                <!-- Display bars below text -->
                {#each tools as tool}
                    <div class="mb-4">
                        <div class="text-sm font-medium mb-1">{tool.name}</div>
                        <div class="w-full bg-gray-700 rounded-full h-3">
                            <div class={tool.color + " h-3 rounded-full flex justify-end items-center pr-2"} style="width: {tool.level}%">
                                <span class="text-xs font-semibold text-white">{tool.label}</span>
                            </div>
                        </div>
                    </div>
                {/each}
            </div>
        {:else}
            {#each tools as tool}
                <div class="mb-4" in:fade={{ duration: 300 }}>
                    <div class="text-sm font-medium mb-1">{tool.name}</div>
                    <div class="w-full bg-gray-700 rounded-full h-3">
                        <div class={tool.color + " h-3 rounded-full flex justify-end items-center pr-2"} style="width: {tool.level}%">
                            <span class="text-xs font-semibold text-white">{tool.label}</span>
                        </div>
                    </div>
                </div>
            {/each}
        {/if}
        <div class="flex justify-center mt-4">
            <button class="btn" on:click={() => toggleExpanded('tools')}>
                {expandedState.tools ? 'Show less ⮝' : 'Show more ⮟'}
            </button>
        </div>
    </div>

    <!-- Programming Languages Card -->
    <div class="card shadow-lg rounded-lg p-4 bg-zinc-800 text-white transition duration-300 ease-in-out transform hover:scale-105 hover:shadow-2xl font-mono">
        <div class="flex justify-center mt-2">
            <h2 class="text-xl font-semibold mb-4">Programming Languages</h2>
        </div>
        {#if expandedState.languages}
            <div class="mt-2 overflow-auto w-60 justify-normal" in:slide={getSlideParams('languages')} out:slide={getSlideParams('languages')}>
                <!-- Display this simple text when expandedState.languages is true -->
                Programming Languages Expertise
                <!-- Display bars below text -->
                {#each languages as language}
                    <div class="mb-4">
                        <div class="text-sm font-medium mb-1">{language.name}</div>
                        <div class="w-full bg-gray-700 rounded-full h-3">
                            <div class={language.color + " h-3 rounded-full flex justify-end items-center pr-2"} style="width: {language.level}%">
                                <span class="text-xs font-semibold text-white">{language.label}</span>
                            </div>
                        </div>
                    </div>
                {/each}
            </div>
        {:else}
            {#each languages as language}
                <div class="mb-4" in:fade={{ duration: 300 }}>
                    <div class="text-sm font-medium mb-1">{language.name}</div>
                    <div class="w-full bg-gray-700 rounded-full h-3">
                        <div class={language.color + " h-3 rounded-full flex justify-end items-center pr-2"} style="width: {language.level}%">
                            <span class="text-xs font-semibold text-white">{language.label}</span>
                        </div>
                    </div>
                </div>
            {/each}
        {/if}
        <div class="flex justify-center mt-4">
            <button class="btn" on:click={() => toggleExpanded('languages')}>
                {expandedState.languages ? 'Show less ⮝' : 'Show more ⮟'}
            </button>
        </div>
    </div>
</div>

<style>
    .btn {
        @apply transition-all duration-500 ease-in-out;
        padding: 5%;
        background-color: #3C4142;
        border-radius: 10px;
    }
    .btn:hover {
        background-color: darkgray;
        color: black;
    }
    .card {
        display: flex;
        flex-direction: column;
        align-self: start; /* Add this line */
        perspective: 1000px;
        width: 100%;
    }
    .card > div:last-child {
        margin-top: auto;
    }
</style>
