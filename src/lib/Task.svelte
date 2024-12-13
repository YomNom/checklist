<script>
    import checkmark from '../../public/checkmark.svg';
    import SubmitButton from './Submit-Button.svelte';

    export let task = "";
</script>

<div class="task">
    <form class="task-form"> 
        <input type = "text" bind:value={task} class = "task-input">
        <SubmitButton />
        <!--
        <button type = "submit" class="submission-button">
            <img src={checkmark} alt="Checkmark Icon" class="icon" />
        </button>
        -->
    </form>
</div>  <!-- errand -->

<style>
    .task {
        width: 500px;
        height: 52px;
        padding: 5px;
    }

    .task-form {
        display: flex;
        flex-direction: row;
        align-items: center;
    }

    .task-input {
        width: 400px;
    }
</style>