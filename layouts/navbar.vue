<template>
    <nav class="navbar">
      <div class="navbar-container">
        <!-- <NuxtLink to="/" class="navbar-brand">My Website</NuxtLink> -->
        <ul class="navbar-nav">
          
          <li class="nav-item">
            <NuxtLink to="/" class="nav-link">Comparison Of Two Countries GDP</NuxtLink>
          </li>

          <li class="nav-item">
            <NuxtLink to="/SelectedGDP" class="nav-link">Displaying  Selected Country GDP</NuxtLink>
          </li>

          <li class="nav-item">
            <NuxtLink to="/Table" class="nav-link">Displaying  Table Of Selected Country</NuxtLink>
          </li>
        
        </ul>
      </div>
    </nav>

    <div>
        <slot />
    </div>
  </template>
  
  <script setup>

  </script>
  
  <style >
  .navbar {
    background-color: #333;
    color: #fff;
    padding: 10px 0;
  }
  
  .navbar-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1200px;
    margin: 0 auto;
  }
  
  .navbar-brand {
    font-size: 1.5rem;
    font-weight: bold;
    color: #fff;
    text-decoration: none;
  }
  
  .navbar-nav {
    list-style: none;
    display: flex;
    margin: 0;
    padding: 0;
  }
  
  .nav-item {
    margin-right: 20px;
  }
  
  .nav-link {
    text-decoration: none;
    color: #fff;
    font-weight: bold;
    transition: color 0.3s ease;
  }
  
  .nav-link:hover {
    color: #ffd700;
  }
  </style>
  