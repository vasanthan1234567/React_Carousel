# Ex05 Image Carousel


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

ImageCarousel.jsx

```jsx

import React, { useState, useEffect } from "react";

const ImageCarousel = ({ images, interval = 3000 }) => {
  const [currentIndex, setCurrentIndex] = useState(0);

  const nextImage = () => {
    setCurrentIndex((prevIndex) => (prevIndex + 1) % images.length);
  };

  const prevImage = () => {
    setCurrentIndex(
      (prevIndex) => (prevIndex - 1 + images.length) % images.length
    );
  };

  useEffect(() => {
    const timer = setInterval(nextImage, interval);
    return () => clearInterval(timer);
  }, [interval, images.length]);

  return (
    <div>
      <img
        src={images[currentIndex]}
        alt={`Slide ${currentIndex + 1}`}
      />
      <div>
        <button onClick={prevImage}>Previous</button>
        <button onClick={nextImage}>Next</button>
      </div>
      <div>
        {images.map((_, index) => (
          <button
            key={index}
            onClick={() => setCurrentIndex(index)}
            disabled={index === currentIndex}
          >
            ●
          </button>
        ))}
      </div>
    </div>
  );
};

export default ImageCarousel;


```

App.jsx

```jsx

import React from "react";
import "./App.css";
import ImageCarousel from "./ImageCarousel";

const App = () => {
  const imageList = [
    'https://picsum.photos/1200/800?random=1',
    'https://picsum.photos/1200/800?random=2',
    'https://picsum.photos/1200/800?random=3',
    'https://picsum.photos/1200/800?random=4',
    'https://picsum.photos/1200/800?random=5',
  ];

  return (
    <div>
      <h2>Simple Image Carousel</h2>
      <ImageCarousel images={imageList} interval={3000} />
    </div>
  );
};

export default App;

```

Main.jsx

```jsx

import { useState } from 'react'
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './index.css'
import App from './App.jsx'

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>
)


```

## OUTPUT


<img width="1916" height="1140" alt="Screenshot 2025-11-10 113805" src="https://github.com/user-attachments/assets/92d7eee8-acb2-4da9-ad27-afa1330e9106" />

<img width="1919" height="1142" alt="Screenshot 2025-11-10 113824" src="https://github.com/user-attachments/assets/f570d97e-bad3-4e0f-b70d-6a3f7ef0954c" />


## RESULT
The program for creating Image Carousel using React is executed successfully.
