<template>
  <div class="relative section-padding-y bg-gray-100 dark:bg-gray-1000">
    <product-scroll>
      <pet-plan-card
        slot="scrollItem"
        class="transition-all duration-500 ease-in-out"
        name="card 1"
      />
      <pet-plan-card
        slot="scrollItem"
        class="transition-all duration-500 ease-in-out"
        name="card 2"
      />
      <pet-plan-card
        slot="scrollItem"
        class="transition-all duration-500 ease-in-out"
        name="card 3"
      />
      <pet-plan-card
        slot="scrollItem"
        class="transition-all duration-500 ease-in-out"
        name="card 4"
      />
    </product-scroll>
  </div>
</template>

<script>
export default {}
</script>
