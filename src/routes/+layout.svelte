<script lang="ts">
    import "../app.css"
</script>

<div class="flex flex-col h-screen">
    <div>
        <div class="ml-2 mt-2 float-left">
            <h1 class="text-7xl text-white">Owl or Lark?</h1>
        </div>
        <!---
        <div class="h-auto flex flex-row items-end mr-2 mt-2 float-right">
            <a href="/" class="navitem" id="counts">Counts</a>
            <a href="/form" class="navitem" id="form">Form</a>
            <a href="/controls" class="navitem-last" id="controls">Controls</a>
        </div>
        -->
    </div>

    <span class="flex-grow flex justify-center items-center bg-purple float-none"><slot /></span>
</div>

<style lang="postcss">
    .bg-purple {
        background-color: purple;
    }
</style>
