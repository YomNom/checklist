<script>
    import { createEventDispatcher } from 'svelte';
    import checkmark from '../../public/checkmark.svg';

    export let note_title = "";
    const dispatch = createEventDispatcher();

    function handleSubmit(event) {
        event.preventDefault();
        dispatch('updateTitle', note_title);
    }
</script>

<div class="editpad">
    <form class="align-title" on:submit={handleSubmit}>
        <input type="text" bind:value={note_title} class="title-input" />
        <button type="submit" class="submission-button">
            <img src={checkmark} alt="Checkmark Icon" class="check-icon" />
        </button>
    </form>
</div>

<style>
    .align-title {
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
    }
    .editpad {
        display: flex;
        position: absolute;
        width: 400px;
        height: 5%;
        font-size: .2em;
        align-items: center;
        justify-content: center;
        flex-direction: row;
        background-color: #faf6c3;
        border-left: none;
        border-radius: 0px 5px 0px 0px;
    }

    .submission-button {
        background-color: #06f77e;
        border: 2px solid #000000;
        border-radius: 50%;
        padding: 6px;
        margin: 5px;
    }

    .check-icon {
        width: 20px;
        height: 20px;
    }
</style>