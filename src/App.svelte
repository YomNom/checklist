<script>
  import "./app.css";
  import TaskForm from "./lib/TaskForm.svelte";
  import TaskHistory from "./lib/TaskHistory.svelte";
  import Edit from "/edit-icon.svg";
  import EditTitle from "./lib/EditTitle.svelte";
  import HeaderBar from "./lib/HeaderBar.svelte";
  import DisplayTask from "./lib/DisplayTask.svelte";

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
  let successfulTasks = [
    { name: "Finish reading 'The Great Gatsby'", description: "Completed reading the book", due_date: "2023-10-10" },
    { name: "Submit tax returns", description: "Filed and submitted tax returns", due_date: "2023-10-12" },
    { name: "Organize office desk", description: "Cleaned and organized the office desk", due_date: "2023-10-14" }
  ];
  let failedTasks = [
    { name: "Clean the house", description: "Vacuum, dust, and mop the floors", due_date: "2023-10-10" },
    { name: "Pay bills", description: "Pay electricity and water bills", due_date: "2023-10-12" },
    { name: "Read a book", description: "Finish reading 'The Great Gatsby'", due_date: "2023-10-14" }
  ];
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

<nav>
    <div class="title-bar"> 
      <HeaderBar />
    </div> <!-- title-bar -->
</nav>

<main>
  
  <div class= "content"> 
    <div class="control-panel">   
      <TaskForm on:addTask={addTask} />
      <TaskHistory {successfulTasks} {failedTasks} />
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
      <DisplayTask {tasks} {selectedTask} {successfulTasks} {failedTasks}/>
    </div>
  </div> <!-- content -->
</main>


<style>
  .notepad {
    display: flex;
    width: 350px;
    height: 800px;
    flex-direction: column;
  }
  .notepad-body {
    display: flex;
    width: 320px;
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
    width: 320px;
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
    height: 100px;
    align-items: center;
    justify-content: center;
    background-color: #050052;
    margin-bottom: 10px;
  }

  .task-outline {
    display: flex;
    flex-direction: column;
    width: 800px;
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
    margin-left: 40px;
    
    align-items: center;
    justify-content: left;
    transform: scale(1.3);
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
    border-radius: 5px 0px 0px 5px;
   }
</style>
