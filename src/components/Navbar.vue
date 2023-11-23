<template>
    <nav class="navbar navbar-expand-lg bg-success">
      <div class="container-fluid">
        <!-- Replace "logo.png" with the actual filename of your logo in the assets folder -->
        <router-link to="/">
          <img src="@/assets/logo.png" alt="HomeService Logo" class="navbar-brand logo" />
        </router-link>
  
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
  
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <router-link class="nav-link text-light" to="/">
                Home
              </router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link text-light" to="/about">
                About
              </router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link text-light" to="/contact">
                Contact
              </router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link text-light" to="/profile">
                Profile
              </router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </template>
  
  <script>
  export default {
    name: "Navbar",
  };
  </script>
  
  <style scoped>
  .logo {
    max-height: 40px; /* Adjust the maximum height of the logo as needed */
  }
  </style>
  