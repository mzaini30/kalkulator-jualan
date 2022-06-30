<template>
  <div class="bagianAtas h-[50vh]"></div>
  <div
    class="bagianBawah grid text-2xl grid-cols-4 bg-orange-500 h-[50vh] text-white"
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
  @apply hover:bg-yellow-500;
}
.icon {
  @apply mx-auto;
}
</style>
