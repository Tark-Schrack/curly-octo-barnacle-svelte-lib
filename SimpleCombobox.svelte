<script>
    /** @type {{
     * options: any[],
     * inputval: string,
     * selectval: string,
     * disabled: boolean,
     * oninput(ev: Event): void,
     * onclick(ev: Event): void
     * }}
     * */
    let {
        options = $bindable(["1", "2"]),
        inputval = $bindable(""),
        selectval = $bindable(),
        disabled = $bindable(false),
        oninput,
        onclick,
    } = $props();

    $effect(() => {
        if (inputval == "") {
            disabled = true;
        } else {
            disabled = false;
        }
    });
</script>

<main>
    <select bind:value={selectval} {oninput} disabled={!disabled}>
        {#each options as opt}
            <option value={opt}>{opt}</option>
        {/each}
    </select>
    <div class="input">
        <span class="input parent">{inputval}</span>
        <input class="input child" type="text" bind:value={inputval} />
    </div>
    <button {disabled} {onclick}>&check;</button>
</main>

<style lang="scss">
    main {
        display: grid;
    }
    @mixin font() {
        font-size: var(--font-size, 1rem);
        line-height: var(--font-size, 1rem);
        font-family: var(--font-family, "Helvetica");
    }
    select {
        grid-column: 1;
        min-width: var(--min-width, 3rem);
        @include font;
        border-radius: 0;
        border: 1px solid rgb(165, 165, 165);
    }
    .input {
        grid-column: 2;
        display: inline-block;
        position: relative;
        &.parent,
        &.child {
            margin: 0;
            @include font;
        }
        &.parent {
            padding-right: 1ch;
            min-width: var(--min-width, 3rem);
        }
        &.child {
            position: absolute;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
        }
    }
    button {
        grid-column: 3;
        padding: 2px 5px;
    }
</style>
