<script>
    import { onMount } from 'svelte';
    import userCircle from '../../public/user-circle.svg';
  
    let currentTime = new Date();
  
    onMount(() => {
      const interval = setInterval(() => {
        currentTime = new Date();
      }, 1000);
  
      return () => clearInterval(interval);
    });
  
    function formatDate(date) {
      return date.toLocaleString();
    }
  </script>
    
  <div class="nav-container">
    <div class="welcome-section">
      <h2>Welcome to Checklist</h2>
      <button class="user-button">
        <img src={userCircle} alt="User Icon" class="user-icon" />
      </button>
    </div>
    <div class="date-time">
      {formatDate(currentTime)}
    </div>
  </div>
  
  <style>
    .nav-container {
      display: flex;
      z-index: 1000;
      width: 1000px;
      height: 80px; 
      background-color: #eaf6ff;
      justify-content: space-between; 
      align-items: center; 
      border-radius: 15px;
      padding: 0 20px;
    }
  
    .welcome-section {
      display: flex;
      align-items: center;
    }
  
    .user-button {
      margin-left: 20px;
      padding: 10px;
      background-color: transparent;
      border: none;
      cursor: pointer;
    }
  
    .user-icon {
      width: 50px;
      height: 50px;
      margin-left: -10px;
    }
  
    .date-time {
      font-size: 1.2em;
      color: #333;
    }
  </style>