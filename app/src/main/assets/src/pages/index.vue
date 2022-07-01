<template>
  <div class="bagianAtas content-end grid h-[60vh]">
    <div class="tampil text-xl bg-red-100 grid grid-cols-5">
      <button class="col-span-1">-</button>
      <div class="col-span-3 text-right px-2">1.000 x 1</div>
      <button class="col-span-1">+</button>
    </div>
    <div class="tampil text-xl bg-red-100 grid grid-cols-5">
      <button class="col-span-1">-</button>
      <div class="col-span-3 text-right px-2">26.000.000 x 2</div>
      <button class="col-span-1">+</button>
    </div>
  </div>
  <div
    class="bagianBawah grid text-2xl grid-cols-4 bg-orange-500 h-[40vh] text-white"
  >
    <button>7</button>
    <button>8</button>
    <button>9</button>
    <button><div class="i-ooui-arrow-next-rtl icon"></div></button>

    <button>4</button>
    <button>5</button>
    <button>6</button>
    <button><div class="i-ooui-newline-ltr icon"></div></button>

    <button>1</button>
    <button>2</button>
    <button>3</button>
    <button>0</button>
  </div>
</template>

<style scoped="">
.bagianBawah button {
  @apply hover:bg-yellow-500 active:bg-transparent;
}
.icon {
  @apply mx-auto;
}
.tampil > * {
  @apply py-2;
}
.tampil .col-span-1 {
  @apply text-center bg-red-200;
}
</style>
