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

    let mobileFactor = $state(1);
    $effect(function() {
        if (mobile == "Mobile") {
            mobileFactor = 2.2;
        }
        else {
            mobileFactor = 1;
        }
    })
</script>
<svelte:head>
    <title>Coeur</title>
    {#each [1, 2, 3, 4, 5] as num}
        <link rel="preload" as="image" href="/images/landing/{num}.png"/>
        <link rel="preload" as="image" href="/images/landingMobile/{num}.png"/>
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
        padding-top: 50px;
        padding-left: 20px;
        padding-right: 20px;
        grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
        background-color: rgb(255, 66, 161);
        overflow: clip;
        div {
            padding: 20px;
        }
        div:first-child {
            text-align: left;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }
        div:last-child {
            text-align: center;
        }
    }
    #ws {
        background-color: rgb(138, 69, 128);
        z-index: 1;
    }
    #grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
        overflow: clip;
        padding-left: 20px;
        padding-right: 20px;
        z-index: 1;

        div {
            padding: 20px;
        }
    }
    #grid div:first-child {
        text-align: center;
    }
    #grid div:last-child {
        text-align: right;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-end;
    }

    #grid.mobile {
        div:first-child {
            text-align: right;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: flex-end;
            
        }
        div:last-child {
            text-align: center;
        }
    }

    #submit {
        background-color: rgb(129, 19, 65);
        text-align: center;
        position: relative;
    }
</style>
<div id="landing">
    <img src="/images/landing{mobile}/1.png" alt="background"/>
    <img src="/images/landing{mobile}/2.png" style:transform="translateY({charY*0.5*mobileFactor}px)" id="titleLogo" translate="no" alt="Title" class="graphic"/>
    <img src="/images/landing{mobile}/3.png" class="graphic" alt="Orpheus and Heidi" />
    <img src="/images/landing{mobile}/4.png" class="graphic" alt="Pink Wave" id="wave"/>
    <img src="/images/landing{mobile}/5.png" class="graphic" alt="Orpheus's Hands" />
</div>
<div id="ys">
    <div>
        <h1 style:font-size="50px">Make E-Cards</h1>
        <h3>E-Cards should be viewable on the web and engaging!</h3>
        <button style:margin-top="20px" style:width="60%">View requirements for submissions</button>
    </div>
    <div>
        <a href="https://hacklyn.city/orpheus"><img translate="no" src="/images/orpheusCard.png" alt="Demo e-card" style:max-width=90% style:transform="rotate(2deg)"/></a>
        <p>Check out this example! <i>(Click on the image)</i></p>
    </div>
</div> 
<div id="ws">
    <img src="/images/wave1.png" alt="Wave graphic" style:width="100%" style:user-select="none" style:-webkit-user-drag="none"/>
    <div id="grid" class:mobile={mobile != ""}>
        {#if mobile == ""}
        <div>
            <img translate="no" src="/images/sweatshirt.png" alt="Sweatshirt" style:max-width=60% style:height="auto" style:transform="rotate(-2deg)" style:border-radius=30px/>
            <p>Each item requires hearts to purchase. You can earn hearts from your submissions; the amount of hearts for each submission depends on the quality of your project and the duration of time you put into making it.</p>
        </div>
        <div>
            <h1 style:font-size="50px">Earn Prizes</h1>
            <h3>The shop includes heart themed merch and even a Hack Club sweatshirt!</h3>
            <button style:margin-top="20px" style:width="60%">Check out the Shop</button>
        </div>
        {:else}
        <div>
            <h1 style:font-size="50px">Earn Prizes</h1>
            <h3>The shop includes heart themed merch and even a Hack Club sweatshirt!</h3>
            <button style:margin-top="20px" style:width="60%">Check out the Shop</button>
        </div>
        <div>
            <img style:border-radius=30px style="display: flex; align-self: center;" translate="no" src="/images/sweatshirt.png" alt="Sweatshirt" style:max-width=60% style:height="auto" style:transform="rotate(-2deg)"/>
            <p>Each item requires hearts to purchase. You can earn hearts from your submissions; the amount of hearts for each submission depends on the quality of your project and the duration of time you put into making it.</p>
        </div>
        {/if}
    </div>
</div>
<div id="submit">
    <img src="/images/wave2.png" alt="Wave graphic" style:width="100%" style:user-select="none" style:-webkit-user-drag="none"/>

    <h1 style="padding: 20px;">Ready to submit?</h1>
    <p style="margin-bottom: 30px; padding: 20px;">That's great! Our submissions form isn't up yet; however, when it is, you can check back here!</p>
    {#if mobile == ""}
    <img src="/images/envelope.png" alt="Envelope" style="max-width: 500px; transform: rotate(3deg);"/>
    {:else}
    <img src="/images/envelope.png" alt="Envelope" style="max-width: 200px; transform: rotate(3deg);"/>
    {/if}
</div>
