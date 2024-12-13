<script>
    import { createEventDispatcher } from 'svelte';
    import SubmitButton from "./Submit-Button.svelte";
    import { Input, Label, Helper } from 'flowbite-svelte';

    let task = {
        name: "",
        description: "",
        due_date: "",
    };

    let show_task_form = false;
    const dispatch = createEventDispatcher();
    let errorMessage = "";

    function handle_ShowTask() {
        show_task_form = !show_task_form;
    }

    function closeForm() {
        show_task_form = false;
        errorMessage = "";
    }

    function submitForm() {
        if (!task.name.trim()) {
            errorMessage = "Task name is required.";
            return;
        }
        dispatch('addTask', { ...task });
        resetForm();
        closeForm();
    }

    function resetForm() {
        task = {
            name: "",
            description: "",
            due_date: "",
        };
        errorMessage = "";
    }
</script>

<button on:click={handle_ShowTask} class="add-task-button">
    <div class="close-top">+</div>
</button>

{#if show_task_form}
    <div class="task-overlay" on:click={closeForm}></div>
    <div class="task">
        <div class="task-content">
            <button class="close-button" on:click={closeForm}>X</button>
            <form class="task-form" on:submit|preventDefault={submitForm}>
                <div class="row"> 
                    <label for="task-name" class="input-label">Task Name</label>
                    <input type="text" id="task-name" bind:value={task.name} class="task-input" required><br>
                </div>
                <div class="row"> 
                    <label for="task-date" class="input-label">Due Date</label>
                    <input type="date" id="task-date" bind:value={task.due_date} class="task-input" placeholder="Due Date"><br>
                </div>
                <textarea bind:value={task.description} class="info-input" placeholder="Task Description"></textarea>
                {#if errorMessage}
                    <div class="error-message">{errorMessage}</div>
                {/if}
                <button type="submit" class="submit-button">Submit</button>
            </form>
        </div> <!-- task-content -->
    </div> <!-- task -->
{/if}

<style>
    .input-label {
        font-size: 20px;
        margin-right: 10px;
        margin-top: 5px;
    }
    .error-message {
        color: red;
        margin-bottom: 10px;
    }

    .submit-button {
        border: 2px solid orangered;
        width: 80px;
        padding: 5px;
        margin-left: 175px;
        border-radius: 8px;
        font-weight: bold;
        margin-top: 10px;
        color: orangered;
    }

    .close-button {
        position: absolute;
        top: -20px;
        right: 1px;
        padding: 10px;
        font-size: 1.5rem;
        font-weight: bold;
        background: none;
        border: none;
        cursor: pointer;
    }
    .close-top {
        margin-top: -10px;
    }

    .add-task-button {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 60px;
        height: 60px;
        margin: 8px;
        padding: 0;
        background-color: #f7ab06;
        font-size: 3.5rem;
        border: 2.5px solid #000000;
        border-radius: 8px;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), inset 0 1px 0 rgba(255, 255, 255, 0.2);
        transition: all 0.2s ease-in-out;
    }

    .add-task-button:hover {
        background-color: #f7ab06;
        color: #704a02;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), inset 0 1px 0 rgba(255, 255, 255, 0.2);
        transform: translateY(-2px);
    }

    .task-overlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.5);
        z-index: 1000;
    }

    .task {
        width: 500px;
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: white;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        z-index: 1001;
    }

    .task-content {
        position: relative;
    }

    .task-form {
        display: flex;
        flex-direction: column;
        align-items: left;
    }

    .task-input {
        width: flex;
    }

    .info-input {
        margin-top: 10px;
        height: 100px;
        resize: none;
    }
</style>