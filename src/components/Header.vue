<style>
  :root {
    --header-height:80px;
  }
  nav {
    padding: 16px 24px;
    background: #262626;
    font-size: 24px;
    color: white;
    box-shadow: 0px 3px 3px #303030;
    letter-spacing: 1px;
  }
  .header-app {
    height: var(--header-height);
  }
</style>

<template>
  <header>
    <nav class="navbar navbar-expand-lg navbar-dark header-app">
    <a class="navbar-brand" href="#">LastMusic</a>
  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item">
        <a class="nav-link" href="#">Lien</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#" >Lien</a>
      </li>
    </ul>
  </div>
   <a class="nav-link login-nav-link" href="#">Login/Register</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
    </nav>
  </header>
</template>

