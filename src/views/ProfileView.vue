<template>
  <div class="profile-container">
    <!-- Add the image from the assets folder -->
    <img src="@/assets/profile-picture.jpg" alt="My Profile Picture" class="profile-picture" />
    <h2>Mochammad Ryan Putra Hermawan</h2>
  </div>

  <div class="social-media">
    <!-- Custom social media logos from assets -->
    <img
      src="@/assets/facebook-logo.jpg"
      alt="Facebook Logo"
      class="social-logo"
      @click="openSocialMedia('https://www.facebook.com/ryan.hermawan.1804109/')"
    />
    <img
      src="@/assets/instagram-logo.jpg"
      alt="Instagram Logo"
      class="social-logo"
      @click="openSocialMedia('https://www.instagram.com/ryanputra3728/')"
    />
    <img
      src="@/assets/x-logo.jpg"
      alt="X Logo"
      class="social-logo"
      @click="openSocialMedia('https://twitter.com/ryanputra3728')"
    />
    <img
      src="@/assets/linkedin-logo.jpg"
      alt="LinkedIn Logo"
      class="social-logo"
      @click="openSocialMedia('https://www.linkedin.com/in/mochammad-ryan-putra-hermawan-7476ab223/')"
    />
    <img
      src="@/assets/github-logo.jpg"
      alt="Github Logo"
      class="social-logo"
      @click="openSocialMedia('https://github.com/Ryanputra3728')"
    />
    <!-- Add more social media logos as needed -->
  </div>
</template>

<script>
export default {
  name: "AboutPage",
  methods: {
    openSocialMedia(url) {
      window.open(url, "_blank");
    },
  },
};
</script>

<style scoped>
.profile-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  height: 50vh; /* Adjust the height to your preference */
}

.profile-picture {
  max-width: 20%; /* Ensure the image does not exceed its natural size */
  height: auto; /* Maintain the aspect ratio of the image */
  margin-top: 20px; /* Add spacing between the heading and the image */
  border-radius: 50%;
}

.social-media {
  display: flex;
  justify-content: center;
  margin-top: -10px; /* Adjust spacing between profile and social media logos */
}

.social-logo {
  width: 30px; /* Adjust the width of social media logos */
  height: 30px; /* Adjust the height of social media logos */
  margin: 0 10px; /* Adjust spacing between social media logos */
  cursor: pointer; /* Add a pointer cursor to indicate the logo is clickable */
}
</style>
