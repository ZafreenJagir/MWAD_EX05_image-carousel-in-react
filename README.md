# MWAD_EX05_image-carousel-in-react
##### Date: 20-11-2025
##### Refister Number : 212223040252
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

App.jsx
```
import React, { useEffect, useState } from "react";
import "./imageComponent.css";

const images = [
  {
    id: 1,
    url: "https://images.pexels.com/photos/29089597/pexels-photo-29089597/free-photo-of-stunning-autumn-beach-sunset-with-waves.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2",
  },
  { id: 2, url: "https://images.pexels.com/photos/691668/pexels-photo-691668.jpeg" },
  {
    id: 3,
    url: "https://images.pexels.com/photos/2049422/pexels-photo-2049422.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2",
  },
  {
    id: 4,
    url: "https://images.pexels.com/photos/325044/pexels-photo-325044.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2",
  },
  {
    id: 5,
    url: "https://images.pexels.com/photos/1485894/pexels-photo-1485894.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2",
  },
];

const ImageCarousel = () => {
  const [currentImageIndex, setCurrentImageIndex] = useState(0);

  const handlePreviousClick = () => {
    setCurrentImageIndex(
      currentImageIndex === 0 ? images.length - 1 : currentImageIndex - 1
    );
  };

  const handleNextClick = () => {
    setCurrentImageIndex((currentImageIndex + 1) % images.length);
  };

  useEffect(() => {
    const timer = setTimeout(() => {
      handleNextClick();
    }, 5000);

    return () => clearTimeout(timer);
  }, [currentImageIndex]);

  return (
    <section>
      <h2>React Image Carousel</h2>

      <div className="image-container">
        <button className="nav-button left" onClick={handlePreviousClick}>
          &lt;
        </button>

        {images.map((image, index) => (
          <img
            src={image.url}
            alt="img"
            className={currentImageIndex === index ? "block" : "hidden"}
            key={image.id}
          />
        ))}

        <button className="nav-button right" onClick={handleNextClick}>
          &gt;
        </button>
      </div>
    </section>
  );
};

const SimpleForm = () => {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [helper, setHelper] = useState("");
  const [error, setError] = useState("");

  const handleEmailChange = (e) => {
    const value = e.target.value;
    setEmail(value);

    const emailRegex = /\S+@\S+\.\S+/;
    if (!emailRegex.test(value)) {
      setError("Invalid email format");
    } else {
      setError("");
    }
  };

  return (
    <div className="form-container">
      <h2>Simple Login Form</h2>

      <input
        type="email"
        placeholder="Enter email"
        value={email}
        onFocus={() => setHelper("Enter a valid email")}
        onChange={handleEmailChange}
      />
      <p className="helper">{helper}</p>
      <p className="error">{error}</p>

      <input
        type="password"
        placeholder="Enter password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />

      <button>Submit</button>
    </div>
  );
};

const App = () => {
  return (
    <div>
      <ImageCarousel />
      <SimpleForm />
    </div>
  );
};

export default App;


```


imageComponent.css

```
.image-container {
  position: relative;
  width: 500px;
  height: 300px;
  margin: auto;
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  position: absolute;
}

.hidden {
  display: none;
}

.block {
  display: block;
}

.nav-button {
  position: absolute;
  top: 50%;
  background-color: black;
  color: white;
  padding: 10px;
  cursor: pointer;
  border: none;
  font-size: 20px;
}

.left {
  left: 10px;
}

.right {
  right: 10px;
}

.form-container {
  margin-top: 40px;
  text-align: center;
}

.helper {
  color: blue;
  font-size: 14px;
}

.error {
  color: red;
  font-size: 14px;
}


```

## OUTPUT

<img width="832" height="833" alt="Screenshot 2025-11-20 193404" src="https://github.com/user-attachments/assets/61e20768-e8a6-48a3-8d0b-15e69849e986" />

<img width="730" height="784" alt="Screenshot 2025-11-20 193411" src="https://github.com/user-attachments/assets/6a9ce0e9-8cb0-4f4b-b3e8-6b76e561cbc0" />

<img width="729" height="764" alt="Screenshot 2025-11-20 193416" src="https://github.com/user-attachments/assets/e6634dac-5949-491b-a6f4-c58daabfad00" />

<img width="764" height="802" alt="Screenshot 2025-11-20 193422" src="https://github.com/user-attachments/assets/245d3ea4-77f5-425d-bc91-bb4a8a9f5de6" />

<img width="721" height="756" alt="Screenshot 2025-11-20 193428" src="https://github.com/user-attachments/assets/7788f74a-ad5a-4658-8161-c235eb1d7b37" />

## RESULT
The program for creating Image Carousel using React is executed successfully.
