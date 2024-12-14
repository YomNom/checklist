<script>
    import historyIcon from '../../public/history-icon.svg';
    export let successfulTasks = [];
    export let failedTasks = [];

    let showHistory = false;
    let filter = "success";

    function handle_ShowHistory() {
        showHistory = !showHistory;
    }
</script>

<button on:click={handle_ShowHistory} class="history-button">
    <div class="close-top">
        <img src={historyIcon} alt="History Icon" class="history-icon" />
    </div>
</button>

{#if showHistory}
    <div class="history-overlay" on:click={handle_ShowHistory}></div>
    <div class="history">
        <div class="history-content">
            <button class="close-button" on:click={handle_ShowHistory}>✖</button>
            <h2>Task History</h2>
            <select bind:value={filter} name="task_type" id="task-type">
                <option value="success">Successful Tasks</option>
                <option value="failed">Failed Tasks</option>
            </select>
            <div class="task-list">
                {#if filter === 'success'}
                    <div>
                        <ul>
                            {#each successfulTasks as task}
                                <div class="task-item">
                                    <li>{task.name}</li>
                                    <div class="item-format">Due date: {task.due_date}</div>
                                    <li>Description: {task.description}</li>
                                </div>
                            {/each}
                        </ul>
                    </div>
                {:else}
                    <div>
                        <ul>
                            {#each failedTasks as task}
                                <div class="failed-task-item">
                                    <li>{task.name}</li>
                                    <div class="item-format">Due date: {task.due_date}</div>
                                    <li>Description: {task.description}</li>
                                </div>
                            {/each}
                        </ul>
                    </div>
                {/if}
            </div>
        </div> <!-- history-content -->
    </div> <!-- history -->
{/if}

<style>
    .failed-task-item {
        background-color: #c90404;
        margin: 10px;
        padding: 10px;
        color: white;
        border-radius: 8px;
    }
    .task-item {
        background-color: #33a107;
        margin: 10px;
        padding: 10px;
        color: white;
        border-radius: 8px;
    }
    .task-list {
        display: flex;
        align-items: left;
        justify-content: left;
        text-align: left;
        width: 660px;
        height: 460px;
        padding: 10px;
        margin-top: 10px;
        overflow-y: auto;
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
        margin-top: 0px;
    }

    .history-button {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 60px;
        height: 60px;
        margin: 8px;
        padding: 0;
        background-color: #e2e1df;
        font-size: 3.5rem;
        border: 2.5px solid #000000;
        border-radius: 8px;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), inset 0 1px 0 rgba(255, 255, 255, 0.2);
        transition: all 0.2s ease-in-out;
    }

    .history-button:hover {
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), inset 0 1px 0 rgba(255, 255, 255, 0.2);
        transform: translateY(-2px);
    }

    .history-overlay {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.5);
        z-index: 1000;
    }

    .history {
        width: 500px;
        height: 600px;
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

    .history-content {
        display: flex;
        flex-direction: column;
        position: relative;
    }
</style>