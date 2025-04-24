# 🎯 JavaScript Event Handling & Interactive Elements Assignment

Welcome to the **ultimate JavaScript playground**! 🎉 This assignment is where we turn boring web pages into dynamic, responsive, *alive* experiences. Get ready to master **event handling**, build **interactive components**, and validate forms like a pro! 💪

## 📁 Assignment Structure

```
📂 js-event-assignment/
├── index.html         # Your playground – where it all comes together
├── style.css          # Keep it cute (optional but encouraged)
└── script.js          # The JavaScript wizardry happens here
```

---

## 🧪 What to Build

Here’s what your interactive bundle of joy should include:

### 1. Event Handling 🎈  
- Button click ✅  
- Hover effects ✅  
- Keypress detection ✅  
- Bonus: A secret action for a *double-click* or *long press* 🤫

### 2. Interactive Elements 🎮  
- A button that changes text or color  
- An image gallery or slideshow  
- Tabs or accordion-style content  
- Bonus: Add some animation using JS or CSS ✨

### 3. Form Validation 📋✅  
- Required field checks  
- Email format validation  
- Password rules (e.g., min 8 characters)  
- Bonus: Real-time feedback while typing

---

## 🧙‍♂️ Pro Tips

- Keep your code clean and commented – your future self will thank you!
- Think about **user experience** – what makes your site more *fun* to use?
- Don’t be afraid to **Google and experiment** – that’s how real developers roll!

---

## 🎉 Now Go Make It Fun!

Remember – this isn't just code. It's your **first step toward creating magical user experiences**. So play around, break stuff (then fix it), and most of all, have FUN! 😄

Happy Coding! 💻✨  

ANSWER
// script.js

// 1. Event Handling 🎈
const clickButton = document.getElementById('click-button');
const hoverArea = document.getElementById('hover-area');
const keypressInput = document.getElementById('keypress-input');
const keypressOutput = document.getElementById('keypress-output');
const doubleLongButton = document.getElementById('double-long-button');
const secretAction = document.getElementById('secret-action');

clickButton.addEventListener('click', () => {
    alert('Button Clicked! 🎉');
});

hoverArea.addEventListener('mouseover', () => {
    hoverArea.textContent = '👋 Hello!';
});

hoverArea.addEventListener('mouseout', () => {
    hoverArea.textContent = 'Hover Over Me';
});

keypressInput.addEventListener('keypress', (event) => {
    keypressOutput.textContent = `You typed: ${event.key}`;
});

let clickCount = 0;
let longPressTimer;

doubleLongButton.addEventListener('mousedown', () => {
    longPressTimer = setTimeout(() => {
        secretAction.classList.remove('hidden');
        setTimeout(() => {
            secretAction.classList.add('hidden');
        }, 2000);
        clickCount = 0; // Reset click count after long press
    }, 1000); // Adjust time for long press (in milliseconds)
});

doubleLongButton.addEventListener('mouseup', () => {
    clearTimeout(longPressTimer);
    clickCount++;
    if (clickCount === 2) {
        secretAction.classList.remove('hidden');
        setTimeout(() => {
            secretAction.classList.add('hidden');
        }, 2000);
        clickCount = 0;
    }
});

doubleLongButton.addEventListener('mouseout', () => {
    clearTimeout(longPressTimer);
    clickCount = 0;
});

// 2. Interactive Elements 🎮
const changeButton = document.getElementById('change-button');
const buttonOutput = document.getElementById('button-output');
let isTextChanged = false;

changeButton.addEventListener('click', () => {
    if (isTextChanged) {
        buttonOutput.textContent = 'Initial Text';
        changeButton.textContent = 'Change Text';
    } else {
        buttonOutput.textContent = 'Text Changed! ✨';
        changeButton.textContent = 'Revert Text';
    }
    isTextChanged = !isTextChanged;
});

const galleryImage = document.getElementById('gallery-image');
const prevImageButton = document.getElementById('prev-image');
const nextImageButton = document.getElementById('next-image');
const images = [
    "https://via.placeholder.com/300/007bff/FFFFFF?Text=Image%201",
    "https://via.placeholder.com/300/28a745/FFFFFF?Text=Image%202",
    "https://via.placeholder.com/300/dc3545/FFFFFF?Text=Image%203"
];
let currentImageIndex = 0;

function updateGalleryImage() {
    galleryImage.src = images[currentImageIndex];
    galleryImage.alt = `Image ${currentImageIndex + 1}`;
}

prevImageButton.addEventListener('click', () => {
    currentImageIndex = (currentImageIndex - 1 + images.length) % images.length;
    updateGalleryImage();
});

nextImageButton.addEventListener('click', () => {
    currentImageIndex = (currentImageIndex + 1) % images.length;
    updateGalleryImage();
});

const accordionHeaders = document.querySelectorAll('.accordion-header');

accordionHeaders.forEach(header => {
    header.addEventListener('click', () => {
        const content = header.nextElementSibling;
        const isOpen = content.style.display === 'block';

        // Close all other open accordion items
        document.querySelectorAll('.accordion-content').forEach(otherContent => {
            if (otherContent !== content) {
                otherContent.style.display = 'none';
            }
        });

        // Toggle the current content
        content.style.display = isOpen ? 'none' : 'block';
    });
});

// Bonus: Animation is done via CSS hover on .animated-box

// 3. Form Validation 📋✅
const signupForm = document.getElementById('signup-form');
const usernameInput = document.getElementById('username');
const emailInput = document.getElementById('email');
const passwordInput = document.getElementById('password');
const usernameError = document.getElementById('username-error');
const emailError = document.getElementById('email-error');
const passwordError = document.getElementById('password-error');
const formSubmissionMessage = document.getElementById('form-submission-message');

function validateEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
}

function validatePassword(password) {
    return password.length >= 8;
}

usernameInput.addEventListener('input', () => {
    if (!usernameInput.value) {
        usernameError.textContent = 'Username is required.';
    } else {
        usernameError.textContent = '';
    }
});

emailInput.addEventListener('input', () => {
    if (!emailInput.value) {
        emailError.textContent = 'Email is required.';
    } else if (!validateEmail(emailInput.value)) {
        emailError.textContent = 'Invalid email format.';
    } else {
        emailError.textContent = '';
    }
});

passwordInput.addEventListener('input', () => {
    if (!passwordInput.value) {
        passwordError.textContent = 'Password is required.';
    } else if (!validatePassword(passwordInput.value)) {
        passwordError.textContent = 'Password must be at least 8 characters long.';
    } else {
        passwordError.textContent = '';
    }
});

signupForm.addEventListener('submit', (event) => {
    let isValid = true;

    if (!usernameInput.value) {
        usernameError.textContent = 'Username is required.';
        isValid = false;
    }

    if (!emailInput.value) {
        emailError.textContent = 'Email is required.';
        isValid = false;
    } else if (!validateEmail(emailInput.value)) {
        emailError.textContent = 'Invalid email format.';
        isValid = false;
    }

    if (!passwordInput.value) {
        passwordError.textContent = 'Password is required.';
        isValid = false;
    } else if (!validatePassword(passwordInput.value)) {
        passwordError.textContent = 'Password must be at least 8 characters long.';
        isValid = false;
    }

    if (isValid) {
        formSubmissionMessage.textContent = '🎉 Form submitted successfully!';
        formSubmissionMessage.classList.remove('hidden');
        signupForm.reset();
        setTimeout(() => {
            formSubmissionMessage.classList.add('hidden');
        }, 3000);
    } else {
        event.preventDefault(); // Prevent form submission if validation fails
    }
});
