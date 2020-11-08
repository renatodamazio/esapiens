<template>
  <div>
    <Nuxt />
  </div>
</template>

<style>
  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box !important;
    outline: none;
    font-family: 'Poppins', sans-serif;
    text-decoration: none;
    color: var(--text-base);
  }

  :root {
    --text-base: #2c3e50;
    --color-primary: 25,91,255;
    --color-primary-light: 244,247,248;
    --color-danger: 255,71,87;
    --color-warning: 255,186,0;
    --color-success: 70,201,58;
    --color-dark: 30,30,30;
    --space-sm: 8px;
    --space-md: 12px;
    --space-lg: 24px;
    --transition-default: .500s ease-in-out;
    --text-size: 16px;
    --text-sm: 12px;
    --text-md: 24px;
    --text-lg: 32px;
  }

  html, body, #__nuxt, #__layout {
    width: 100%;
    height: 100%;
    font-size: 1rem;
  }

  .container {
    width: 100%;
    height: 100vh;
    padding: 10px;
    /* border: 1px solid #000; */
  }

  a {
    font-weight: 400;
    transition: .300s ease-in-out;
  }

  a:hover {
    color: rgb(var(--color-primary));
  }

  .avatar {
    border-radius: 100%;
  }

  hr {
    border: 1px solid rgb(var(--color-primary-light));
  }
</style>
