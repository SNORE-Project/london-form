<script lang="ts">
    import Question from "$lib/Question.svelte";
    import FlipCard from "$lib/FlipCard.svelte";
    import lark_img from "$lib/assets/lark.png";
    import neutral_img from "$lib/assets/neutral.png";
    import owl_img from "$lib/assets/owl.png";

    function is_highest(n1: number, n2: number, n3: number): boolean {
        return n1 > n2 && n1 > n3;
    }

    function reload() {
        window.scrollTo(0,0);

        let form = document.querySelector("#form");
        if (form == null) {
            console.log("error: form not found");
            return;
        }

        (form as HTMLFormElement).reset();

        setTimeout(set_invisible, 1000);
    }

    function set_lark() {
        src = lark_img;
        text = lark_text;
        alt = "Lark image";
    }

    function set_owl() {
        src = owl_img;
        text = owl_text;
        alt = "Owl image";
    }

    function set_neutral() {
        src = neutral_img;
        text = neutral_text;
        alt = "Neutral image";
    }

    function set_visible() {
        let hidden = document.querySelector<HTMLElement>("#hidden");
        if (hidden != null) {
            hidden.style.display = "block";
        }
    }

    function set_invisible() {
        let hidden = document.querySelector<HTMLElement>("#hidden");
        if (hidden != null) {
            hidden.style.display = "";
        }
    }

    const lark_text =
`The Sleep Charity advises:

You are more of a Lark.

This means that you like to go to bed earlier and get up earlier.

You cannot train yourself to be an Owl if you are a Lark. It’s a genetic predisposition. However you can try coping strategies to deal with the effects of going against your natural body clock.

It is important to remember to not get hung up on sleep quantity, but focus on sleep quality.`;

    const owl_text =
`The Sleep Charity advises:

You are more of an Owl.

This means that you like to go to bed later and get up later.

You cannot train yourself to be a Lark if you are an Owl. It’s a genetic predisposition. However you can try coping strategies to deal with the effects of going against your natural body clock.

It is important to remember to not get hung up on sleep quantity, but focus on sleep quality.`;

    const neutral_text =
`The Sleep Charity advises:

You are a neither a Lark nor an Owl.

This means that you are more adaptable to sleep schedules.

You cannot train yourself to be an Owl or a Lark. It’s a genetic predisposition. However you can try coping strategies to deal with the effects of going against your natural body clock.

It is important to remember to not get hung up on sleep quantity, but focus on sleep quality.`;

    let src = "";
    let alt = "";
    let text = "";

    function submit(event: Event) {
        if (event.target instanceof HTMLFormElement) {
            const form_data = new FormData(event.target);
            
            let owl_count = 0;
            let neutral_count = 0;
            let lark_count = 0;
            for (let field of form_data) {
                if (field[1] == "owl") {
                    owl_count++; 
                } else if (field[1] == "neutral") {
                    neutral_count++;
                } else if (field[1] == "lark") {
                    lark_count++;
                }
            }

            if (is_highest(neutral_count, owl_count, lark_count) || owl_count == lark_count) {
                set_neutral();
            } else if (is_highest(owl_count, lark_count, neutral_count)) {
                set_owl();
            } else if (is_highest(lark_count, neutral_count, owl_count) || lark_count == neutral_count) {
                set_lark();
            } else if (owl_count == neutral_count) {
                set_owl();
            }

            set_visible();

            window.scrollTo(0, document.body.scrollHeight);
        }
    }
</script>

<div class="w-screen bg-slate-50 m-6 py-1 px-2">
    <form on:submit|preventDefault={submit} id="form">
        <Question q="If you could get up when you choose, would you prefer to wake:"
            lark="Bright and early, before 7.30am"
            neutral="Between 7.30am and 9am, you don't want to waste the day"
            owl="After 9am, you love having a lie in" num=1 />
        <Question q="How easy do you find getting up in the morning?"
            lark="Very easy. I get up with no problems"
            neutral="Neither particularly easy or difficult"
            owl="Really difficult. I prefer to stay under the duvet as long as possible" num=2 />
        <Question q="Do you need an alarm to wake you in the morning?"
            lark="No, I'm generally awake"
            neutral="Yes, I'm fairly dependent on an alarm"
            owl="Definitely, or I'd keep on snoozing" num=3 />
        <Question q="Imagine that you have no commitments tomorrow, what time would you choose to go to bed compared to your usual bedtime?"
            lark="Same time as usual"
            neutral="An hour or so later"
            owl="I'd stay up and go to bed several hours later" num=4 />
        <Question q="How alert do you feel for the first half hour after you've woken?"
            lark="Very alert"
            neutral="Somewhat alert"
            owl="Not at all alert" num=5 />
        <Question q="If you had to take a test, what time of the day would you sit it?"
            lark="First thing in the morning"
            neutral="Just before lunch"
            owl="As late in the day as possible" num=6 />
        <Question q="If a friend signed you up for a class that you were really keen to join but it was taking place at 10pm each evening, how would you feel?"
            lark="Gutted, that's far too late!"
            neutral="It's not ideal, but you'd attend"
            owl="Thrilled, you can't wait to start attending" num=7 />

        <button type="submit" class="text-xl button">Submit</button>
    </form>

    <div id="hidden" class="w-96">
        <p class="desktop mt-6 text-lg">Hover to see a description of your chronotype</p>
        <p class="mobile">Tap to see a description of your chronotype</p>
        <FlipCard {src} {text} {alt} />
        <div class="w-full flex flex-row">
            <button type="button" class="text-xl button" on:click={reload}>Reset form</button>
        </div>
    </div>
</div>

<style lang="postcss">
    #hidden {
        display: none;
    }

    .button {
        @apply bg-slate-200 hover:bg-purple-600 active:bg-purple-400 hover:text-white
            active:text-white border-2 border-black rounded transition-all
            px-2 py-1;
        flex-grow: 1;
    }
</style>
