<template>
  <div class="row">
    <div class="col-sm">
      <vue-carousel  :data="data"></vue-carousel>
      <div class="text-center">Left (default)</div>
    </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      data: [
        '<div class="example-slide">Slide 1</div>',
        '<div class="example-slide">Slide 2</div>',
        '<div class="example-slide">Slide 3</div>',
      ],
    };
  },
};
</script>

<style>
.example-slide {
  align-items: center;
  background-color: #6669;
  color: rgb(180, 178, 178);
  display: flex;
  font-size: 1.5rem;
  justify-content: center;
  min-height: 10rem;
  min-width: 10rem;
}
</style>