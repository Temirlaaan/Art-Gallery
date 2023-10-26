<template>
  <div>
    <h1>Art Gallery, made by Temirlan</h1>

    <select v-model="selectedMuseum" class="custom-select">
      <option value="">All Museums</option>
      <option v-for="museum in museums" :value="museum" :key="museum">{{ museum }}</option>
    </select>

    <div class="image-gallery">
      <div
        v-for="image in filteredImages"
        :key="image.id"
        class="image-container"
        @mouseover="animateImage(image.id)"
        @mouseout="resetAnimation(image.id)"
        @click="openLightbox(image)"
      >
        <img :src="image.src" :alt="image.title" />
      </div>
    </div>

    <div v-if="lightboxOpen" class="lightbox">
      <span class="close-button" @click="closeLightbox">&times;</span>
      <img :src="selectedImage.src" :alt="selectedImage.title" class="lightbox-image" />
    </div>
  </div>
</template>

<script>


export default {
  data() {
    return {
      museums: ['Rijk Museum', 'The Met Museum', 'Japanese Prints', 'Nasa Archives'],
      images: [
        { id: 1, src: 'image1.jpg', museum: 'Rijk Museum', title: 'Artwork 1' },
        { id: 2, src: 'image2.jpg', museum: 'Rijk Museum', title: 'Artwork 2' },
        { id: 3, src: 'image3.jpg', museum: 'Rijk Museum', title: 'Artwork 3' },
        { id: 4, src: 'image4.jpg', museum: 'Rijk Museum', title: 'Artwork 4' },
        { id: 5, src: 'image5.jpg', museum: 'Rijk Museum', title: 'Artwork 5' },
        { id: 6, src: 'image6.jpg', museum: 'The Met Museum', title: 'Artwork 6' },
        { id: 7, src: 'image7.jpg', museum: 'The Met Museum', title: 'Artwork 7' },
        { id: 8, src: 'image8.jpg', museum: 'The Met Museum', title: 'Artwork 8' },
        { id: 9, src: 'image9.jpg', museum: 'The Met Museum', title: 'Artwork 9' },
        { id: 10, src: 'image10.jpg', museum: 'Japanese Prints', title: 'Artwork 10' },
        { id: 11, src: 'image11.jpg', museum: 'Japanese Prints', title: 'Artwork 11' },
        { id: 12, src: 'image12.jpg', museum: 'Japanese Prints', title: 'Artwork 12' },
        { id: 13, src: 'image13.jpg', museum: 'Japanese Prints', title: 'Artwork 13' },
        { id: 14, src: 'image14.jpg', museum: 'Japanese Prints', title: 'Artwork 14' },
        { id: 15, src: 'image15.jpg', museum: 'Nasa Archives', title: 'Artwork 10' },
        { id: 16, src: 'image16.jpg', museum: 'Nasa Archives', title: 'Artwork 11' },
        { id: 17, src: 'image17.jpg', museum: 'Nasa Archives', title: 'Artwork 12' },
        { id: 18, src: 'image18.jpg', museum: 'Nasa Archives', title: 'Artwork 13' },
        { id: 19, src: 'image19.jpg', museum: 'Nasa Archives', title: 'Artwork 14' },
        
      ],
      selectedMuseum: '',
      hoveredImage: null,
      lightboxOpen: false,
      selectedImage: {},
    };
  },

  computed: {
    filteredImages() {
      if (this.selectedMuseum) {
        return this.images.filter(image => image.museum === this.selectedMuseum);
      } else {
        return this.images;
      }
    },
  },
  methods: {
  animateImage(imageId) {
    this.hoveredImage = imageId;
  },
  resetAnimation() {
    this.hoveredImage = null;
  },
  openLightbox(image) {
    this.selectedImage = image;
    this.lightboxOpen = true;
  },
  closeLightbox() {
    this.lightboxOpen = false;
  },
}

};
</script>

<style scoped>
.image-gallery {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}


.image-container {
  position: relative;
  transition: transform 0.2s ease-in-out;
  cursor: pointer;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
}

.image-container img {
  max-width: 200px;
  max-height: 200px;
}

.image-container:hover {
  transform: scale(1.05);
}

.lightbox {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.lightbox-image {
  max-width: 90%;
  max-height: 90%;
}


.close-button {
  position: absolute;
  top: 20px;
  right: 20px;
  font-size: 24px;
  color: #fff;
  cursor: pointer;
  background-color: rgba(0, 0, 0, 0.3); 
  padding: 5px 10px; 
  border: 1px solid #fff;
  border-radius: 50%; 
  transition: background-color 0.3s, transform 0.3s;
}

.close-button:hover {
  background-color: rgba(255, 255, 255, 0.5); 
  transform: scale(1.1); 
}


.custom-select {
  margin: 10px;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
</style>
