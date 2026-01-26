<script>
    import { onMount } from "svelte";

    let mobile = $state("");
    let charY = $state(0);
    onMount(() => {
        if (window.innerWidth <= 800) {
            mobile = "Mobile";
        }
        else {
            mobile = "";
        }
        window.addEventListener("resize", function() {
            if (this.window.innerWidth <= 800) {
                mobile = "Mobile";
            }
            else {
                mobile = "";
            }
        })
    })
</script>
<svelte:head>
    <title>Coeur</title>
    {#each [1, 2, 3, 4, 5] as num}
        <link rel="preload" as="image" href="/images/landing/{num}.png"/>
    {/each}
</svelte:head>
<svelte:window bind:scrollY={charY}></svelte:window>
<style>
    .graphic {
        transform-origin: bottom center;
    }
    
    #landing {
        overflow: clip;
        position: relative;
        user-select: none;
        -webkit-user-drag: none;
        img {
            position: absolute;
            user-select: none;
            -webkit-user-drag: none;
            bottom: 0;
            top: auto;
            right: 0;
            left: 0;
        }
    } 

    #landing img:first-child {
        position: relative;
        display: block;
        z-index: 0;
    }

    #wave {
        animation: wave 5s infinite ease-in-out;
    }

    @keyframes wave {
        0% {
            transform: translateY(0);
        }
        50% {
            transform: translateY(12px);
        }
        100% {
            transform: translateY(0px);
        }
    }
 
    #ys {
        display: grid;
        grid-template-columns: auto auto;
        column-gap: 10px;
    }
</style>
<div id="landing">
    <img src="/images/landing{mobile}/1.png" alt="background"/>
    <img src="/images/landing{mobile}/2.png" style:transform="translateY({charY*0.5}px)" id="titleLogo" alt="Title" class="graphic"/>
    <img src="/images/landing{mobile}/3.png" class="graphic" alt="Orpheus and Heidi" />
    <img src="/images/landing{mobile}/4.png" class="graphic" alt="Pink Wave" id="wave"/>
    <img src="/images/landing{mobile}/5.png" class="graphic" alt="Orpheus's Hands" />
</div>
<div id="ys">
    <div>
        <h2>Make E-Cards</h2>
    </div>
    <div>
        <h3>E-Cards should be viewable on the web and engaging!</h3>
        <button>View requirements for submissions</button>
    </div>
</div>
