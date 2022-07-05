<script setup="" lang="ts">
// idAktif
// id, nilai, banyak
import { Ref, ref, onUpdated } from "vue";
import Swal from "sweetalert2";
const { stringify, parse } = JSON;

type List = {
  id: number;
  nilai: string;
  banyak: number;
};

const list: Ref<List[]> = ref([
  {
    id: 1,
    nilai: "",
    banyak: 1,
  },
]);
const total: Ref<number> = ref(0);
const aktif: Ref<number> = ref(1);
const jalankanScroll: Ref<boolean> = ref(false);

function init() {
  if (localStorage.list) {
    list.value = parse(localStorage.list);
  }
  if (localStorage.total) {
    total.value = parse(localStorage.total);
  }
}
init();

function tambahList(): void {
  const idBaru = Math.random();
  list.value.push({
    id: idBaru,
    nilai: "",
    banyak: 1,
  });
  aktif.value = idBaru;
  jalankanScroll.value = true;
}
function tambah(angka: string): void {
  for (let x of list.value) {
    if (x.id == aktif.value) {
      x.nilai += angka;
    }
  }
}
function hapus(): void {
  for (let x of list.value) {
    if (x.id == aktif.value) {
      x.nilai = x.nilai.slice(0, -1);
    }
  }
}
function hilangkan(id: number): void {
  list.value = list.value.filter((x) => x.id != id);
}
async function mauReset() {
  const tanya = await Swal.fire("Reset kah?");
  if (tanya.isConfirmed) {
    list.value = [
      {
        id: 1,
        nilai: "",
        banyak: 1,
      },
    ];
    aktif.value = 1;
  }
}
onUpdated(() => {
  if (jalankanScroll.value == true) {
    const target = document.querySelector(".bagianAtas");
    if (target) {
      target.scrollTop = target.scrollHeight;
    }
    jalankanScroll.value = false;
  }
  let kumpulinTotal = 0;
  for (let x of list.value) {
    kumpulinTotal += +x.nilai * x.banyak;
  }
  total.value = kumpulinTotal;
  localStorage.list = stringify(list.value);
  localStorage.total = stringify(total.value);
});
</script>

<template>
  <div class="bagianAtas content-between grid h-[50vh] overflow-auto w-full">
    <div></div>
    <div>
      <div
        v-for="x in list"
        :key="x.id"
        class="tampil text-xl bg-red-100 grid grid-cols-5"
        @click="aktif = x.id"
      >
        <button
          class="col-span-1"
          @click="x.banyak > -1 ? x.banyak-- : hilangkan(x.id)"
        >
          -
        </button>
        <div
          class="col-span-3 text-right px-2"
          :class="x.id == aktif ? 'bg-green-500 text-white' : null"
        >
          {{ (+x.nilai).toLocaleString("id") || 0 }} x {{ x.banyak }}
        </div>
        <button class="col-span-1" @click="x.banyak++">+</button>
      </div>
    </div>
  </div>
  <div class="h-[50vh]">
    <div class="tampil flex justify-between text-xl bg-red-100">
      <button class="px-2 bg-yellow-500 text-white" @click="mauReset">
        reset
      </button>
      <div class="px-2">
        {{ total.toLocaleString("id") }}
      </div>
    </div>
    <div class="bagianBawah grid text-2xl grid-cols-4 bg-orange-500 text-white">
      <button @click="tambah('7')">7</button>
      <button @click="tambah('8')">8</button>
      <button @click="tambah('9')">9</button>
      <button @click="hapus">
        <div class="i-ooui-arrow-next-rtl icon"></div>
      </button>

      <button @click="tambah('4')">4</button>
      <button @click="tambah('5')">5</button>
      <button @click="tambah('6')">6</button>
      <button @click="tambahList">
        <div class="i-ooui-newline-ltr icon"></div>
      </button>

      <button @click="tambah('1')">1</button>
      <button @click="tambah('2')">2</button>
      <button @click="tambah('3')">3</button>
      <button @click="tambah('0')">0</button>
    </div>
  </div>
</template>

<style scoped="">
.bagianBawah button {
  @apply hover:bg-yellow-500 active:bg-transparent;
}
.bagianBawah {
  height: calc(50vh - 44px);
}
.icon {
  @apply mx-auto;
}
.tampil > * {
  @apply py-2;
}
.tampil .col-span-1 {
  @apply text-center bg-red-200 hover:bg-red-300 active:bg-red-200;
}
</style>
