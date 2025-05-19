# Ex05 Image Carousel
## Date: 19-05-2025

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
## Carousel.js
```
import React, { useState, useEffect } from 'react';
import './Carousel.css';

const Carousel = ({ images }) => {
  const [currentIndex, setCurrentIndex] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setCurrentIndex((prevIndex) => (prevIndex + 1) % images.length);
    }, 4000);
    return () => clearInterval(interval);
  }, [images.length]);

  const goToPrevious = () => {
    setCurrentIndex((prevIndex) =>
      prevIndex === 0 ? images.length - 1 : prevIndex - 1
    );
  };

  const goToNext = () => {
    setCurrentIndex((prevIndex) =>
      prevIndex === images.length - 1 ? 0 : prevIndex + 1
    );
  };

  return (
    <div className="carousel">
      <div className="carousel-image-container">
        <img
          src={images[currentIndex]}
          alt={`Slide ${currentIndex}`}
          className="carousel-image"
        />
        <button onClick={goToPrevious} className="carousel-button left">❮</button>
        <button onClick={goToNext} className="carousel-button right">❯</button>
      </div>
      <div className="carousel-dots">
        {images.map((_, index) => (
          <span
            key={index}
            className={`dot ${index === currentIndex ? 'active' : ''}`}
            onClick={() => setCurrentIndex(index)}
          />
        ))}
      </div>
    </div>
  );
};

export default Carousel;

```
## Carousel.css
```
.carousel {
    max-width: 700px;
    margin: 0 auto;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 0 30px rgba(255, 0, 0, 0.4);
  }
  
  .carousel-image-container {
    position: relative;
    height: 400px;
  }
  
  .carousel-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: opacity 0.6s ease-in-out;
    border-radius: 10px;
  }
  
  .carousel-button {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: rgba(255, 0, 0, 0.5);
    color: #fff;
    border: none;
    padding: 12px 20px;
    font-size: 24px;
    cursor: pointer;
    border-radius: 50%;
    z-index: 2;
  }
  
  .carousel-button:hover {
    background: rgba(255, 0, 0, 0.8);
  }
  
  .carousel-button.left {
    left: 15px;
  }
  
  .carousel-button.right {
    right: 15px;
  }
  
  .carousel-dots {
    text-align: center;
    padding: 10px 0;
  }
  
  .dot {
    display: inline-block;
    width: 14px;
    height: 14px;
    margin: 0 5px;
    background: #888;
    border-radius: 50%;
    cursor: pointer;
  }
  
  .dot.active {
    background: red;
  }
  
```
## App.js
```
import React from 'react';
import Carousel from './Carousel';
import './App.css';

function App() {
  const images = [
    process.env.PUBLIC_URL + '/images/img1.png',
    process.env.PUBLIC_URL + '/images/img2.png',
    process.env.PUBLIC_URL + '/images/img3.png',
    process.env.PUBLIC_URL + '/images/img4.png',
  ];

  return (
    <div className="App">
      <video autoPlay loop muted className="video-bg">
        <source src={process.env.PUBLIC_URL + '/videos/bg.mp4'} type="video/mp4" />
        Your browser does not support the video tag.
      </video>

      <div className="content-overlay">
        <h1 className="title">Stranger Things Carousel</h1>
        <p className="subtitle">Enter the Upside Down</p>
        <Carousel images={images} />
        <footer>
          <p>Created by: DEEPIKA S</p>
          <p>Register Number: 212222230028</p>
        </footer>
      </div>
    </div>
  );
}

export default App;

```
## App.css
```
@import url('https://fonts.googleapis.com/css2?family=Creepster&display=swap');

body, html {
  margin: 0;
  padding: 0;
  font-family: 'Creepster', cursive;
  overflow-x: hidden;
  height: 100%;
}

.App {
  position: relative;
  width: 100%;
  height: 100vh;
  color: #fff;
  text-align: center;
}

.video-bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: -1;
  opacity: 1;
  filter: brightness(50%);
}

.content-overlay {
  position: relative;
  z-index: 1;
  padding-top: 50px;
}

.title {
  font-size: 50px;
  color: red;
  text-shadow: 0 0 10px #ff0000;
  margin-bottom: 10px;
}

.subtitle {
  font-size: 20px;
  margin-bottom: 30px;
  color: #bbb;
}

footer {
  margin-top: 30px;
  font-size: 14px;
  color: #ccc;
}

```
## OUTPUT
![stranger1 1](https://github.com/user-attachments/assets/ebc42dd1-4c0a-42ba-aa80-1a9514149841)
![stranger1](https://github.com/user-attachments/assets/c03b80c6-921f-4b5a-9bb1-bc4ed6ff9ca5)
![stranger 1 3](https://github.com/user-attachments/assets/9f2fcbed-b974-4909-bebd-1b35e00404dd)


## RESULT
The program for creating Image Carousel using React is executed successfully.
