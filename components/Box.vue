<template>
  <div class="box"><slot /></div>
</template>

<style scoped>
.box {
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  transition: box-shadow 0.3s ease;
}
.box:hover {
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.05),
    0px 6px 10px rgba(0, 0, 0, 0.03);
}
</style>
