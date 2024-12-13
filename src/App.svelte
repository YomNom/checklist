<script>
  import "./app.css";
  import TaskForm from "./lib/TaskForm.svelte";
  import Edit from "/edit-icon.svg";
  import EditTitle from "./lib/EditTitle.svelte";

  let task = {
        name: "",
        description: "",
        due_date: "",
  };
  let tasks = [
    {
      name: "Buy groceries",
      description: "Milk, Bread, Cheese, Eggs",
      due_date: "2023-10-15"
    },
    {
      name: "Complete project report",
      description: "Finalize the project report and send it to the manager",
      due_date: "2023-10-20"
    },
    {
      name: "Workout",
      description: "Go to the gym for a workout session",
      due_date: "2023-10-18"
    }
  ]; // Array of task

  let selectedTask = null;
  let note_title = "To-Do List";
  let show_title_edit = false;

  function handleRadioClick(index) {
    if (selectedTask === index) {
      selectedTask = null;
    } else {
      selectedTask = index;
    }
  }

  function addTask(event) {
    const newTask = event.detail;
    tasks = [...tasks, newTask];
  }

  function handle_ShowTitleEdit() {
    show_title_edit = !show_title_edit;
  }

  function updateTitle(event) {
    note_title = event.detail;
    show_title_edit = false;
  }
</script>

<main>
  <nav>
    <div class="title-bar"> 
    </div> <!-- title-bar -->
  </nav>
  <div class= "content"> 
    <div class="control-panel">   
      <TaskForm on:addTask={addTask} />
    </div> <!-- control-panel -->
    <div class="notepad">
      <div class="notepad-header">
        <h2>{note_title}</h2>
        <button on:click={handle_ShowTitleEdit}>
          <img src={Edit} alt="Edit Icon" class="icon" />
        </button>

        {#if show_title_edit}
          <EditTitle {note_title} on:updateTitle={updateTitle} />
        {/if}

      </div> <!-- notepad-header -->
      <div class="notepad-body">
        <form class="task-list"> 
          {#each tasks as task, i}
            <label class="task-item">
              <input type="radio" name="example1" value={i} on:click={() => handleRadioClick(i)} checked={selectedTask === i}>
              <div class="item-format">{task.name}</div>
            </label>
          {/each}
        </form>
      </div> <!-- notepad-body --> 
    </div> <!-- notepad -->
    <div class="task-outline"> 

    </div>
  </div> <!-- content -->
</main>


<style>
  .notepad {
    display: flex;
    width: 600px;
    height: 800px;
    flex-direction: column;
  }
  .notepad-body {
    display: flex;
    width: 500px;
    height: 92%;
    align-items: left;
    justify-content: left;
    padding-top: 10px;
    background-color: #faf6c3;
    border-bottom: 1px solid #4fa77b;
    border-right: 1px solid #4fa77b;
    border-top: 1px solid #4fa77b;
    border-radius: 0px 0px 5px 0px;
  } 
  .notepad-header {
    display: flex;
    width: 500px;
    height: 8%;
    align-items: center;
    justify-content: center;
    background-color: #faf6c3;
    border: 1px solid #4fa77b;
    border-left: none;
    border-radius: 0px 5px 0px 0px;
  }

  .title-bar {
    display: flex;
    width: 100%;
    height: 50px;
    align-items: center;
    justify-content: center;
    background-color: #4fa77b;
    border: 1px solid #4fa77b;
    margin-bottom: 10px;
  }

  .task-outline {
    display: flex;
    flex-direction: column;
    width: 300px;
    height: 800px;
    align-items: center;
    justify-content: center;
    border-radius: 0px 5px 5px 0px;
  } 

  .task-list { 
    display: flex;
    flex-direction: column;
  }
  .task-item {
    display: flex;
    margin-bottom: 20px;
    margin-left: 80px;
    
    align-items: center;
    justify-content: left;
    transform: scale(1.5);
  }
  .item-format {
    margin-left: 10px;
  }

  .content {
    display: flex;
    flex-direction: row;
    justify-content: center;
   }

   .control-panel {
    display: flex;
    flex-direction: column;
    background-color: #faf6c3;
    border: 1px solid #4fa77b;
    border-right: 2px solid #b31026;
   }
</style>
