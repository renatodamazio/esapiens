<template>
  <div>
    <search/>

    <Nuxt />
  </div>
</template>
<script>
export default {
  components: {
    Search: () => import('@/components/Search.vue')
  }
}
</script>
<style>
  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box !important;
    outline: none;
    font-family: 'Poppins', sans-serif;
    text-decoration: none;
    color: var(--text-base);
    list-style: none;
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

  .flex {
    display: flex;
  }

  .mb-sm {
    margin-bottom: var(--space-sm);
  }

  .mb-lg {
    margin-bottom: var(--space-lg);
  }
  
  .mt-sm {
    margin-top: var(--space-sm);
  }

  .mt-lg {
    margin-top: var(--space-lg);
  }

  /* ----- */
  .pr-sm {
    padding-right: var(--space-sm);
  }
  /* ----- */


  .text-sm {
    font-size: var(--space-sm);
  }

  .text-md {
    font-size: var(--space-md);
  }

  .text-lg {
    font-size: var(--space-lg);
  }

  .justify-between {
    justify-content: space-between;
  }

  .justify-end {
    justify-content: flex-end;
  }

  .align-center {
    align-items: center;
  }

  .tag {
    padding: var(--space-sm);
    border: 1px solid rgb(var(--color-dark));
    border-radius: 4px;
    font-size: 1rem;
    background: var(--color-primary-light);
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

  .section {
    width: 100%;
    float: left;
  }

  .list-default  {
    padding: var(--space-sm);
  }

  .list-default li {
    border-bottom: 1px solid #eee;
    padding: var(--space-sm);
    color: var(--text-base);
  }

  .text-center {
    text-align: center;
  }
</style>
