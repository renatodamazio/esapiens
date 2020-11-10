<template>
  <div class="welcome">
    <h1>Bem vindo ao sistema de busca do GitHub</h1>
  </div>
</template>
<style scoped>
    .welcome {
      width: 100%;
      height: calc(100vh - 90px);
      text-align: center;
      padding: 50px; 
      z-index: -1;
      position: relative;
    }

    .welcome:before {
      content: "";
      width: 100%;
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
      opacity: 0.2;
      background: url('/github-octocat@1200x630.png') center/contain no-repeat;
    }

    .welcome h1 {
      opacity: 0.9;
      z-index: 1;
      /* color: rgb(var(--color-primary)); */
      position: absolute;
      top: 50%;
      width: 100%;
      left: 0;
      text-align: center;
      transform: translateY(-50%);
      transition: 44.900s ease-in-out;
      /* animation-delay: .403s; */
      animation: animate-text .400s forwards;
    }


    @keyframes animate-text {
      0% {
        opacity: 0;
        transform: translateY(25%);
      }

      100% {
        opacity: 1;
        transform: translateY(-50%);
      }
    }
</style>
<script>
export default {
  mounted() {
  },

  methods: {
    
  }
}
</script>

