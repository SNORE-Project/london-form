<script lang="ts">
    export let lark: string;
    export let neutral: string;
    export let owl: string;
    export let q: string;
    export let num: string;
</script>

<div class="flex flex-col mb-4">
    <h1 class="text-xl font-bold">{q}</h1>
    <label class="label"><input type="radio" name="q{num}" value="lark" required> {lark}</label>
    <label class="label"><input type="radio" name="q{num}" value="neutral" required> {neutral}</label>
    <label class="label"><input type="radio" name="q{num}" value="owl" required> {owl}</label>
</div>

<style lang="postcss">
    .label {
        @apply pl-6 transition-all hover:text-purple-600
    }
</style>
