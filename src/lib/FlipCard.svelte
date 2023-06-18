<script lang="ts">
    export let src: string;
    export let text: string;
    export let alt: string;
</script>

<div class="w-96 h-96 perspective mt-2 mb-2" id="outer">
    <div class="transition-transform duration-[0.6s] text-center" id="inner">
        <div class="border-2 border-purple-900 rounded" id="front">
            <img {src} {alt} />
        </div>

        <div class="border-2 border-orange-500 rounded" id="back">
            <p class="p-4">{text}</p>
        </div>
    </div>
</div>

<style lang="postcss">
    .perspective {
        perspective: 1000px;
    }

    #inner {
        position: relative;
        width: 100%;
        height: 100%;
        transform-style: preserve-3d;
    }

    #outer:hover #inner {
        transform: rotateY(180deg);
    }

    #front, #back {
        position: absolute;
        backface-visibility: hidden;
        -webkit-backface-visibility: hidden;
        -moz-backface-visibility: hidden;
        width: 100%;
        height: 100%;
    }

    #back {
        background-color: purple;
        transform: rotateY(180deg);
        color: white;
        white-space: pre-wrap;
    }
</style>
