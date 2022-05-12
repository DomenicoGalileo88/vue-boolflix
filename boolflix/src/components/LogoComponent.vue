<template>
  <div class="logo_boolflix">
    <a href="#"
      ><img src="@/assets/img/logo_boolflix.png" alt="logo_boolflix"
    /></a>
  </div>
</template>

<script>
export default {
  name: "LogoBoolflix",
};
</script>

<style lang="scss" scoped>
.logo_boolflix {
  &:hover {
    animation: swing 500ms linear;
  }

  @keyframes swing {
    25% {
      transform: rotate(10deg);
    }
    50% {
      transform: rotate(-10deg);
    }
    75% {
      transform: rotate(10deg);
    }
    100% {
      transform: rotate(0);
    }
  }
}
</style>
