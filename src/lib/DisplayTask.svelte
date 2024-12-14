<script>
    export let tasks = [];
    export let selectedTask = null;
    export let successfulTasks = [];
    export let failedTasks = [];
    
    let taskBox;
    let container;
  
    function handleDragStart(event) {
      event.dataTransfer.setData('text/plain', null); // Required for Firefox
      taskBox.style.opacity = '0.5';
    }
  
    function handleDragEnd(event) {
      taskBox.style.opacity = '1';
    }
  
    function handleDragOver(event) {
      event.preventDefault();
    }
  
    function handleDrop(event) {
      event.preventDefault();
      const containerRect = container.getBoundingClientRect();
      const taskBoxRect = taskBox.getBoundingClientRect();
      let left = event.clientX - containerRect.left - taskBoxRect.width / 2;
      let top = event.clientY - containerRect.top - taskBoxRect.height / 2;
  
      // Restrict movement within container
      left = Math.max(0, Math.min(left, containerRect.width - taskBoxRect.width));
      top = Math.max(0, Math.min(top, containerRect.height - taskBoxRect.height));
  
      taskBox.style.left = `${left}px`;
      taskBox.style.top = `${top}px`;
    }
  </script>
  
  <div class="container" bind:this={container}>
    <img src="/corkboard.jpg" alt="Corkboard" class="corkboard" />
    <!-- svelte-ignore a11y-no-static-element-interactions -->
     {#if selectedTask === null}
        <h1>Select a Task to see more details</h1>
      {:else}
        <div
        class="task-box"
        draggable={selectedTask !== null}
        on:dragstart={handleDragStart}
        on:dragend={handleDragEnd}
        on:dragover={handleDragOver}
        on:drop={handleDrop}
        bind:this={taskBox}
        >
        {#if selectedTask === null}
            <h1>Select a Task to see more details</h1>
        {:else}
            <h3>{tasks[selectedTask].name}</h3>
            <p class="highlight-text">Due Date: {tasks[selectedTask].due_date}</p>
            <p>{tasks[selectedTask].description}</p>
        {/if}
        </div> <!-- task-box -->
     {/if}
    <div class="action-board">
        <button class= "success-button" on:click={() => selectedTask = null}>
            <div class="success-icon">✔</div>
        </button>
        <button class="fail-task-button" on:click={() => selectedTask = null}>
            <div class="fail-task-icon">✖</div>
        </button>
    </div>
  </div>
  
  <style>
    .success-button {
        width: 350px;
        height: 140px;
        background-color: rgb(16, 160, 16);
        color: white;
        font-size: 6em;
        border-radius: 10px;
        margin-right: 30px;
    }
    .fail-task-button {
        width: 350px;
        height: 140px;
        background-color: red;
        color: white;
        font-size: 6em;
        border-radius: 10px;
        margin-left: 30px;
    }
    .action-board {
        display: flex;
        flex-direction: row;
        position: absolute;
        bottom: 0px;
        left: 50%;
        transform: translateX(-50%);
        padding: 10px;
        border-radius: 10px;
    }

    .container {
      position: relative;
      width: 100%;
      height: 100vh;
      overflow: hidden;
    }
  
    .corkboard {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 80%;
      object-fit: cover;
      border: 10px solid brown;
      border-radius: 15px;
      z-index: -1; /* Ensure the corkboard is behind other content */
    }
  
    .task-box {
      width: 340px;
      min-height: 270px;
      padding: 20px;
      background-color: yellow;
      margin-left: 245px;
      margin-top: 100px;
      position: absolute;
      cursor: move;
      user-select: none; /* Prevent text selection */
    }
  
    .container h1 {
      background-color: #f5f5f5;
      padding: 20px;
      width: 300px;
      margin-left: 245px;
      margin-top: 100px;
      position: absolute;
      border: none;
    }

    .task-box h3 {
      margin: 0 0 10px 0;
      font-size: 1.5em;
      font-weight: bold;
    }
  
    .task-box p {
      margin: 5px 0;
    }
  
    .highlight-text {
      font-size: 1.2em;
      background-color: rgb(34, 233, 7);
    }
  </style>