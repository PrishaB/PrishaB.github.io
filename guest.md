
<style>
@use postcss-preset-env {
  stage: 0;
}
/*
All grid code is placed in a 'supports' rule (feature query) at the bottom of the CSS (Line 77).
The 'supports' rule will only run if your browser supports CSS grid.
Flexbox is used as a fallback so that browsers which don't support grid will still recieve an identical layout.
*/
@import url(https://fonts.googleapis.com/css?family=Montserrat:500);
:root {
  /* Base font size */
  font-size: 10px;
}
*,
*::before,
*::after {
  box-sizing: border-box;
}
body {
  min-height: 100vh;
  background: linear-gradient(45deg, #49a09d, #5f2c82);
}


.navbar {
background-color: transparent;
}

.container {
  max-width: 100rem;
  margin: 0 auto;
  padding: 0 2rem 2rem;
}
.heading {
  font-family: "Montserrat", Arial, sans-serif;
  font-size: 4rem;
  font-weight: 500;
  line-height: 1.5;
  text-align: center;
  padding: 3.5rem 0;
  color: white;
}
.heading span {
  display: block;
}
.gallery {
  display: flex;
  flex-wrap: wrap;
  /* Compensate for excess margin on outer gallery flex items */
  margin: -1rem -1rem;
}
.gallery-item {
  /* Minimum width of 24rem and grow to fit available space */
  flex: 1 0 24rem;
  /* Margin value should be half of grid-gap value as margins on flex items don't collapse */
  margin: 1rem;
  box-shadow: 0.3rem 0.4rem 0.4rem rgba(0, 0, 0, 0.4);
  overflow: hidden;
}
.gallery-image {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 400ms ease-out;
}
.gallery-image:hover {
  transform: scale(1.15);
}
/*
The following rule will only run if your browser supports CSS grid.
Remove or comment-out the code block below to see how the browser will fall-back to flexbox styling.
*/
@supports (display: grid) {
  .gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(24rem, 1fr));
    grid-gap: 2rem;
  }
  .gallery,
  .gallery-item {
    margin: 0;
  }
}
</style>
<div class="container">
<h1 class="heading">Image Gallery <span> </span></h1>
<div class="gallery">
  <div class="gallery-item">
      <img class="gallery-image" src="/images/photo8.jpg" alt=" ">
    </div>
  <div class="gallery-item">
      <img class="gallery-image" src="/images/photo9.jpg" alt=" ">
    </div>
  <div class="gallery-item">
      <img class="gallery-image" src="/images/photo4.jpg" alt=" ">
    </div>
  <div class="gallery-item">
      <img class="gallery-image" src="/images/photo5.jpg" alt=" ">
    </div>
  <div class="gallery-item">
      <img class="gallery-image" src="/images/photo7.jpg" alt=" ">
    </div>
  <div class="gallery-item">
      <img class="gallery-image" src="/images/photo6.jpg" alt=" ">
    </div>
  <div class="gallery-item">
      <img class="gallery-image" src="/images/b&w3.jpg" alt=" ">
    </div>
  <div class="gallery-item">
      <img class="gallery-image" src="/images/b&w2.jpg" alt=" ">
    </div>
  <div class="gallery-item">
      <img class="gallery-image" src="/images/b&w1.jpg" alt=" ">
    </div>

 </div>
</div>


<!-- <script>
function ArrayList<String> getFiles() {
    
    result = document.getElementById("isLeapYearResult");

    // Fetch data from API
    fetch('https://serafina.tk/api/downloadFiles')
    .then(response => response.json())
    .then(data => {

        console.log(data);

        result.innerHTML = "Is " + yearParam + " a leap year: ";

    })
}

</script> -->