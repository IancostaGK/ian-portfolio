<script setup lang="ts">
const {x, y} = useMouse()
const {width, height} = useWindowSize()

const dx = computed(() => Math.abs(x.value - width.value / 2))
const dy = computed(() => Math.abs(y.value - height.value / 2))
const distance = computed(() => Math.sqrt(dx.value ** 2 + dy.value ** 2))
const size = computed(() => Math.max(300 - distance.value / 3, 150))

const logo = ref<HTMLElement>()
const opacity = computed(() => Math.min(Math.max(size.value / 300, 0.7), 1))
const logoGradient = computed(() => {
  let rect = logo.value?.getBoundingClientRect()
  const xPos = x.value - (rect?.left ?? 0)
  const yPos = y.value - (rect?.top ?? 0)

  return `radial-gradient(circle at ${xPos}px ${yPos}px, black 30%, transparent 100%)`
})
</script>

<template>
  <div class="h-screen w-screen flex justify-center items-center bg-gradient-to-b from-black to-green-500/30 from-80% relative overflow-hidden">
    <div class="absolute bg-green-500/30 rounded-full -translate-x-1/2 -translate-y-1/2 pointer-events-none blur-3xl"
      :style="{
        opacity,
        left: `${x}px`,
        top: `${y}px`,
        width: `${size}px`,
        height: `${size}px`,
      }"
    />

    <div :style="{maskImage: logoGradient}" ref="logo" class="flex-col space-y-4 w-96 text-center">
      <h3 class="text-3xl">
        Frontend Developer
      </h3>

      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Iste quisquam ea, dicta perferendis in esse odit? Minus quis in corporis ipsam, eos beatae temporibus rem adipisci commodi? Id, quo quos.
      </p>
      <p>
        Ian Santos
      </p>
    </div>
  </div>
</template>

<style scoped>

</style>