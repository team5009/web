<script lang="ts">
    import {onMount} from 'svelte'
    import { browser } from '$app/environment'
    import { Canvas } from '@threlte/core'
    import type { Size } from '@threlte/core';
    import { Jellyfish } from 'svelte-loading-spinners'
    import Scene from './Scene.svelte'

    let CanvasSize: Size
    let scroll: number
    let loading = true

    onMount(() => {
        CanvasSize = {
            width: window.innerWidth,
            height: window.innerHeight
        }
        loading = false
    })
</script>
<svelte:window
    on:resize={() => CanvasSize = {width: window.innerWidth, height: 600}}
    bind:scrollY={scroll}
/>
{#if !browser}
    <section class="loading">
        <Jellyfish size={100} color="white"/>
    </section>
{:else}
    <section class="title" >
        <h1 id="title-outside" style='top: calc(50% - {scroll * 0.3}px);'>HELIOS</h1>
        <div class="Canvas-Container" style='top: -{scroll * 0.35}px;'>
            <Canvas size={CanvasSize}>
                <Scene size={CanvasSize} scroll={scroll}/>
            </Canvas>
        </div>
        <h1 id="title-inside" style='top: calc(50% - {scroll * 0.3}px);'>HELIOS</h1>
        <h1 id="title-glow" style='top: calc(50% - {scroll * 0.3}px);'>HELIOS</h1>
    </section>
    <section class="wrapper" style='top: {scroll} - 100vh;'>
        <div class="container"></div>
        <div class="container"></div>
        <div class="container"></div>
        <div class="container"></div>
        <div class="container"></div>
        <div class="container"></div>
        <div class="container"></div>
        <div class="container"></div>
    </section>

    <div>{scroll}</div>
{/if}


<style>
    
    .loading {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }

    .title {
        position: fixed;
        top: 0;
        left: 0;
        width: 100vw;
        height: 100vh;
        color: white;
        pointer-events: none;
    }
    .title h1 {
        margin: 0;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 10vw;
        font-weight: 900;
        text-transform: uppercase;
        text-align: center;
        letter-spacing: 1.25rem;
    }
    #title-outside {
        z-index: 3;
        -webkit-text-fill-color: transparent;
        -webkit-text-stroke-width: 0.2rem;
    }
    #title-inside {
        z-index: 1;
        text-shadow: 0 0 10px white;
        opacity: 1;
    }

    #title-glow {
        z-index: 0;
        filter: blur(2rem);
    }
    .Canvas-Container {
        position: relative;
        z-index: 2;
    }

    .wrapper {
        position: absolute;
        left: 0;
        top: 100vh;
        width: 100vw;
        pointer-events: none;
    }

    .wrapper .container {
        width: 100vw;
        height: 100vh;
        background-color: black;
    }
</style>