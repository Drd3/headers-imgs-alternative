<template>
  <div :id="galleryID" class="gallery-container">
    <a
      v-for="(image, key) in imagesData"
      :key="key"
      :href="image.largeURL"
      :data-pswp-width="image.width"
      :data-pswp-height="image.height"
      target="_blank"
      rel="noreferrer"
    >
      <img :src="image.thumbnailURL" alt="" />
    </a>
  </div>
</template>

<script>
import PhotoSwipeLightbox from 'photoswipe/lightbox';
import 'photoswipe/style.css';

export default {
  name: 'SimpleGallery',
  props: {
    galleryID: String,
    images: Array,
  },
  setup(props) {
    return {
      imagesData: props.images,
    };
  },
  mounted() {
    if (!this.lightbox) {
      this.lightbox = new PhotoSwipeLightbox({
        gallery: '#' + this.$props.galleryID,
        children: 'a',
        pswpModule: () => import('photoswipe'),
      });
      this.lightbox.init();
    }
  },
  unmounted() {
    if (this.lightbox) {
      this.lightbox.destroy();
      this.lightbox = null;
    }
  },
  methods: {},
};
</script>

<style>
.gallery-container {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  grid-template-rows: 140px 140px;
  max-width: 600px;
  margin: auto;
  gap: .6rem;
  border-radius: 10px;
  overflow: hidden;
}

a:first-child{
  grid-row: 1 / span 2;
}

img {
  width: 100%;
  height: 100%;
  position: relative;
  object-fit: cover;
  background: #ccc;
}
</style>
