
---

### **Main Event Listener: `DOMContentLoaded`**

```javascript
document.addEventListener('DOMContentLoaded', () => {
    initAnimations();
    initDarkMode();
    initBackToTop();
    initPreloader();
    initCursorEffects();
    initScrollEvents();
    initCounterAnimation();
    initSidebarToggle();
    certifications();
    initializeCertificationDetailModal();
});
```

**What it does**: This block of code waits for the entire webpage (the HTML document) to fully load before running the functions inside it. Think of it like waiting for all the ingredients to be ready before you start cooking.

- **`document.addEventListener('DOMContentLoaded', () => { ... })`**: This tells the browser, "Hey, don’t run this code until the webpage is completely loaded." The `DOMContentLoaded` event fires when the HTML is fully parsed, but before images or other resources finish loading.
  - **Why?** If you try to manipulate elements (like buttons or sections) before the HTML is loaded, JavaScript won’t find them, and your code will break.
  - **Simple analogy**: It’s like waiting for all the actors to be on stage before starting the play.

- **The arrow function `() => { ... }`**: This is a modern way to write a function in JavaScript. It’s a shorthand for saying, "Here’s a block of code to run when the event happens."
  - **Example**: If you had a button and wanted to show an alert when it’s clicked, you’d write:
    ```javascript
    button.addEventListener('click', () => {
        alert('Button clicked!');
    });
    ```

- **Calling functions**: Inside the arrow function, you call several functions (`initAnimations()`, `initDarkMode()`, etc.). These are like individual tasks you’ve set up to make your website interactive. Each function handles a specific feature (e.g., animations, dark mode, etc.). We’ll explain each one below.

**What to ask if confused**:
- What happens if I don’t wait for `DOMContentLoaded`?
- Why do we need so many functions? Can I combine them?

---

### **1. `initAnimations()`: Adding Animations with Intersection Observer**

```javascript
function initAnimations() {
    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            entry.target.classList.toggle('visible', entry.isIntersecting);
        });
    }, { threshold: 0.2, rootMargin: '0px 0px -10% 0px' });

    document.querySelectorAll('.card, .timeline-wrapper, .circle')
        .forEach(el => observer.observe(el));
}
```

**What it does**: This function makes elements (like cards, timeline items, or tech stack icons) appear with a smooth animation when you scroll to them. It uses something called the **Intersection Observer API**, which watches if elements are visible in the viewport (the part of the webpage you can see).

- **`const observer = new IntersectionObserver((entries) => { ... }, { threshold: 0.2, rootMargin: '0px 0px -10% 0px' })`**: Creates an observer that watches elements. When 20% (`threshold: 0.2`) of an element enters the viewport (adjusted by a small margin), it triggers the code inside.
  - **Simple analogy**: Imagine you’re a teacher watching kids enter a classroom. When a kid is at least 20% inside the door, you mark them as "present." The `rootMargin` is like giving a little extra space around the door to decide when they’re "in."

- **`entries.forEach(entry => { ... })`**: The observer gives you a list (`entries`) of elements it’s watching. For each element (`entry`), you check if it’s visible (`entry.isIntersecting`).
  - **Example**: If you’re watching a card, `entry.isIntersecting` is `true` when the card is visible on the screen.

- **`entry.target.classList.toggle('visible', entry.isIntersecting)`**: If the element is visible (`entry.isIntersecting` is `true`), it adds the CSS class `visible` to the element. If it’s not visible, it removes the `visible` class.
  - **Why?** In your CSS (e.g., `.card.visible`), you’ve defined animations (like fading in or sliding up) that happen when the `visible` class is added.
  - **Simple example**: Imagine you have a light bulb. When you "toggle" the switch on, it lights up. Here, `visible` is like turning on the animation.

- **`document.querySelectorAll('.card, .timeline-wrapper, .circle')`**: Selects all elements with the classes `card`, `timeline-wrapper`, or `circle` (these are your project cards, timeline items, and tech stack icons).
  - **What’s `querySelectorAll`?** It’s like telling JavaScript, "Find all elements that match these classes."
  - **Example**: If you had `<div class="card">`, `querySelectorAll('.card')` would find it.

- **`.forEach(el => observer.observe(el))`**: Tells the observer to start watching each of these elements.
  - **Analogy**: It’s like assigning a security camera to watch each classroom door.

**Why it’s useful**: Instead of animating everything at once (which could slow down the page), this only animates elements when they’re visible, making your site smoother and more engaging.

**What to ask if confused**:
- What’s an Intersection Observer, and why not just use CSS animations?
- How does `threshold` affect when animations start?
- What’s `classList.toggle` doing exactly?

**Simplified example**:
```javascript
// Watch a single div and add a class when it’s visible
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('show');
        }
    });
});
observer.observe(document.querySelector('.my-div'));
```
With CSS:
```css
.my-div {
    opacity: 0;
}
.my-div.show {
    opacity: 1;
    transition: opacity 1s;
}
```

---

### **2. `initDarkMode()`: Toggling Dark Mode**

```javascript
function initDarkMode() {
    const darkModeToggle = document.getElementById('dark-mode-toggle');

    if (localStorage.getItem('darkMode') === 'true') {
        document.body.classList.add('dark-mode');
    }

    darkModeToggle?.addEventListener('click', () => {
        document.body.classList.toggle('dark-mode');
        localStorage.setItem('darkMode', document.body.classList.contains('dark-mode'));
    });
}
```

**What it does**: This function lets users switch between light and dark modes by clicking a button. It also remembers their choice using `localStorage` so the mode persists when they revisit the site.

- **`const darkModeToggle = document.getElementById('dark-mode-toggle')`**: Finds the button with the ID `dark-mode-toggle` (your dark mode button in the HTML).
  - **Why?** You need to know which button the user will click to toggle the mode.

- **`if (localStorage.getItem('darkMode') === 'true') { document.body.classList.add('dark-mode') }`**: Checks if the user previously enabled dark mode (stored in `localStorage`). If so, it adds the `dark-mode` class to the `<body>` tag to apply dark mode styles.
  - **What’s `localStorage`?** It’s like a small notebook the browser keeps to store data (like whether dark mode is on). `localStorage.getItem('darkMode')` reads the value stored under the key `darkMode`.
  - **Example**: If you save your game progress in a video game, `localStorage` is like saving that progress so it’s there when you come back.

- **`darkModeToggle?.addEventListener('click', () => { ... })`**: Adds a click event listener to the dark mode button. The `?.` is a safety check to ensure `darkModeToggle` exists before adding the listener.
  - **Why `?.`?** If the button isn’t found (e.g., wrong ID), it prevents errors.
  - **Analogy**: It’s like checking if a doorbell exists before trying to ring it.

- **`document.body.classList.toggle('dark-mode')`**: Toggles the `dark-mode` class on the `<body>` tag. If it’s there, it’s removed; if it’s not, it’s added.
  - **Why?** Your CSS uses `.dark-mode` to change colors (e.g., background, text) for dark mode.

- **`localStorage.setItem('darkMode', document.body.classList.contains('dark-mode'))`**: Saves the current state (whether `dark-mode` is active) to `localStorage`. If `dark-mode` is on, it saves `'true'`; if off, it saves `'false'`.
  - **Why?** So the user’s preference is remembered next time they visit.

**Why it’s useful**: Dark mode is user-friendly, and saving the preference makes the experience seamless.

**What to ask if confused**:
- What’s `localStorage`, and how is it different from regular variables?
- Why do we need `classList.toggle` instead of just adding the class?
- What does `?.` do, and when should I use it?

**Simplified example**:
```javascript
// Toggle a class on a button click
const button = document.getElementById('my-button');
button.addEventListener('click', () => {
    document.body.classList.toggle('blue-background');
});
```
With CSS:
```css
.blue-background {
    background-color: blue;
}
```

---

### **3. `initBackToTop()`: Back-to-Top Button**

```javascript
function initBackToTop() {
    const backToTopBtn = document.getElementById('back-to-top');

    backToTopBtn?.addEventListener('click', () => {
        window.scrollTo({ top: 0, behavior: 'smooth' });
    });
}
```

**What it does**: This makes the "Back to Top" button scroll the page smoothly to the top when clicked.

- **`const backToTopBtn = document.getElementById('back-to-top')`**: Finds the button with the ID `back-to-top`.

- **`backToTopBtn?.addEventListener('click', () => { ... })`**: Adds a click event listener to the button. The `?.` ensures no error if the button isn’t found.

- **`window.scrollTo({ top: 0, behavior: 'smooth' })`**: Scrolls the window to the top (`top: 0`) with a smooth animation (`behavior: 'smooth'`).
  - **Analogy**: It’s like pressing an elevator button to go to the ground floor smoothly.

**Why it’s useful**: Makes navigation easier on long pages.

**What to ask if confused**:
- What does `window.scrollTo` do, and what’s the `behavior` option?
- Why do we need `?.` here?

**Simplified example**:
```javascript
const button = document.getElementById('go-up');
button.addEventListener('click', () => {
    window.scrollTo({ top: 0, behavior: 'smooth' });
});
```

---

### **4. `initPreloader()`: Hiding the Preloader**

```javascript
function initPreloader() {
    window.addEventListener('load', () => {
        setTimeout(() => {
            document.getElementById('preloader')?.classList.add('hidden');
        }, 300);
    });
}
```

**What it does**: Hides the preloader (a loading animation) after the page fully loads.

- **`window.addEventListener('load', () => { ... })`**: Waits for the entire page (including images, etc.) to load, unlike `DOMContentLoaded`, which only waits for HTML.
  - **Why?** You want the preloader to stay until everything is ready.

- **`setTimeout(() => { ... }, 300)`**: Waits 300 milliseconds (0.3 seconds) before running the code inside.
  - **Why?** Adds a slight delay to make the transition smoother, so the preloader doesn’t disappear too abruptly.

- **`document.getElementById('preloader')?.classList.add('hidden')`**: Adds the `hidden` class to the preloader element to hide it (your CSS defines `.hidden` as `opacity: 0` with `pointer-events: none`).
  - **Analogy**: It’s like turning off a "Loading..." sign once a game is ready.

**Why it’s useful**: Shows a loading animation while the page loads, improving user experience.

**What to ask if confused**:
- What’s the difference between `load` and `DOMContentLoaded`?
- Why use `setTimeout` here?

**Simplified example**:
```javascript
window.addEventListener('load', () => {
    document.getElementById('loader').style.display = 'none';
});
```

---

### **5. `initCursorEffects()`: Custom Cursor**

```javascript
function initCursorEffects() {
    const cursor = document.querySelector('.custom-cursor');
    if (!cursor) return;

    document.addEventListener('mousemove', (e) => {
        cursor.style.transform = `translate(${e.clientX}px, ${e.clientY}px)`;
    });

    document.body.addEventListener('mouseover', (e) => {
        cursor.classList.toggle('hover', e.target.matches('a, button, .card'));
    });
}
```

**What it does**: Creates a custom cursor (a circle that follows the mouse) and changes its appearance when hovering over links, buttons, or cards.

- **`const cursor = document.querySelector('.custom-cursor')`**: Finds the element with the class `custom-cursor` (a div styled as a circle in your CSS).

- **`if (!cursor) return`**: If the cursor element isn’t found, stop the function to avoid errors.
  - **Why?** Prevents the code from breaking on devices where the custom cursor is disabled (e.g., touch devices).

- **`document.addEventListener('mousemove', (e) => { ... })`**: Listens for mouse movement and updates the cursor’s position to follow the mouse.
  - **`cursor.style.transform = translate(${e.clientX}px, ${e.clientY}px)`**: Moves the cursor to the mouse’s position (`e.clientX`, `e.clientY` are the mouse coordinates).
  - **Analogy**: It’s like moving a spotlight to follow an actor on stage.

- **`document.body.addEventListener('mouseover', (e) => { ... })`**: Listens for when the mouse hovers over elements.
  - **`cursor.classList.toggle('hover', e.target.matches('a, button, .card'))`**: Adds or removes the `hover` class when the mouse is over a link (`a`), button, or element with class `card`. Your CSS changes the cursor’s size and style when `.hover` is applied.
  - **What’s `e.target.matches`?** Checks if the hovered element matches the selector (e.g., `a`, `button`, `.card`).
  - **Example**: If you hover over a button, the cursor grows bigger (per your CSS: `.custom-cursor.hover`).

**Why it’s useful**: A custom cursor makes your site feel modern and interactive.

**What to ask if confused**:
- How do `clientX` and `clientY` work?
- What does `matches` do, and how can I use it for other elements?

**Simplified example**:
```javascript
const cursor = document.querySelector('.cursor');
document.addEventListener('mousemove', (e) => {
    cursor.style.left = e.clientX + 'px';
    cursor.style.top = e.clientY + 'px';
});
```

---

### **6. `initScrollEvents()`: Handling Scroll Behavior**

```javascript
function initScrollEvents() {
    window.addEventListener('scroll', debounce(handleScroll, 100));
}

function handleScroll() {
    const scrollY = window.scrollY;

    // Navbar shrink effect
    document.querySelector('.navbar')?.classList.toggle('shrink', scrollY > 50);

    // Back to top visibility
    document.getElementById('back-to-top')?.classList.toggle('visible', scrollY > 300);

    // Active navigation highlighting
    let current = '';
    document.querySelectorAll('section, #home').forEach(section => {
        if (scrollY >= section.offsetTop - 100) {
            current = section.getAttribute('id');
        }
    });

    document.querySelectorAll('.nav-link').forEach(link => {
        link.classList.toggle('active', link.getAttribute('href').substring(1) === current);
    });
}
```

**What it does**: This handles three things when the user scrolls: shrinking the navbar, showing/hiding the back-to-top button, and highlighting the active navigation link.

- **`window.addEventListener('scroll', debounce(handleScroll, 100))`**: Calls `handleScroll` when the user scrolls, but uses `debounce` to limit how often it runs (every 100 milliseconds) to improve performance.
  - **What’s `debounce`?** Explained below in its own section. It’s like saying, "Don’t call me every second while I’m scrolling; wait a bit."

- **`const scrollY = window.scrollY`**: Gets how far the user has scrolled down the page (in pixels).
  - **Example**: If you scroll halfway down a 1000px page, `scrollY` might be 500.

- **Navbar shrink**:
  - **`document.querySelector('.navbar')?.classList.toggle('shrink', scrollY > 50)`**: Adds the `shrink` class to the navbar if the user scrolls more than 50 pixels. Your CSS likely makes the navbar smaller when `.shrink` is applied.

- **Back-to-top visibility**:
  - **`document.getElementById('back-to-top')?.classList.toggle('visible', scrollY > 300)`**: Shows the back-to-top button (adds `visible` class) when the user scrolls more than 300 pixels.

- **Active navigation highlighting**:
  - **`let current = ''`**: Stores the ID of the current section.
  - **`document.querySelectorAll('section, #home').forEach(section => { ... })`**: Loops through all `<section>` elements and the `#home` section.
  - **`if (scrollY >= section.offsetTop - 100)`**: Checks if the user has scrolled past the top of a section (minus 100px for better timing). `offsetTop` is the distance from the top of the page to the section.
  - **`current = section.getAttribute('id')`**: Sets `current` to the section’s ID (e.g., `projects`, `experience`).
  - **`document.querySelectorAll('.nav-link').forEach(link => { ... })`**: Loops through all navigation links.
  - **`link.classList.toggle('active', link.getAttribute('href').substring(1) === current)`**: Adds the `active` class to the link whose `href` (e.g., `#projects`) matches the current section’s ID. `substring(1)` removes the `#` from the `href`.

**Why it’s useful**: Enhances navigation by visually indicating the current section and making the navbar and back-to-top button responsive to scrolling.

**What to ask if confused**:
- What’s `offsetTop`, and how does it know where a section is?
- Why do we need `debounce`?
- How does the `active` class change the nav link’s appearance?

**Simplified example**:
```javascript
window.addEventListener('scroll', () => {
    if (window.scrollY > 100) {
        document.querySelector('nav').classList.add('small');
    } else {
        document.querySelector('nav').classList.remove('small');
    }
});
```

---

### **7. `initCounterAnimation()`: Animating Stat Numbers**

```javascript
function initCounterAnimation() {
    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.querySelectorAll('.stat-number').forEach(stat => {
                    animateCounter(stat, parseInt(stat.getAttribute('data-target')));
                });
                observer.unobserve(entry.target);
            }
        });
    }, { threshold: 0.7 });

    document.querySelectorAll('.stats, .visitor-stats').forEach(section => {
        observer.observe(section);
    });
}

function animateCounter(el, target) {
    const duration = 2000; // animation duration in ms (2 seconds)
    const startTime = performance.now();

    function updateCounter(currentTime) {
        const elapsed = currentTime - startTime;
        const progress = Math.min(elapsed / duration, 1); // value between 0 and 1

        const currentValue = Math.floor(progress * target);
        el.textContent = currentValue;

        if (progress < 1) {
            requestAnimationFrame(updateCounter);
        } else {
            el.textContent = target;
        }
    }

    requestAnimationFrame(updateCounter);
}
```

**What it does**: Animates numbers (like "Years Experience" or "Projects Completed") to count up from 0 to a target value when their section is visible.

- **`const observer = new IntersectionObserver((entries) => { ... }, { threshold: 0.7 })`**: Watches for when 70% of the stats section is visible.
  - **Why 0.7?** Ensures the animation starts only when most of the section is in view.

- **`entries.forEach(entry => { ... })`**: For each observed section, checks if it’s visible (`entry.isIntersecting`).

- **`entry.target.querySelectorAll('.stat-number').forEach(stat => { ... })`**: Finds all elements with class `stat-number` in the visible section and animates them.

- **`animateCounter(stat, parseInt(stat.getAttribute('data-target')))`**: Calls `animateCounter` with the element and its target number (stored in a `data-target` attribute in HTML).
  - **`parseInt`**: Converts the attribute (a string, e.g., `"50"`) to a number (e.g., `50`).

- **`function animateCounter(el, target)`**: Animates the number in `el` to reach `target`.
  - **`const duration = 2000`**: Animation takes 2 seconds.
  - **`const startTime = performance.now()`**: Gets the current time to track animation progress.
  - **`function updateCounter(currentTime)`**: Updates the number every frame.
    - **`const elapsed = currentTime - startTime`**: How much time has passed.
    - **`const progress = Math.min(elapsed / duration, 1)`**: A value from 0 to 1, representing how far along the animation is.
    - **`const currentValue = Math.floor(progress * target)`**: Calculates the current number to display.
    - **`el.textContent = currentValue`**: Updates the element’s text.
    - **`requestAnimationFrame(updateCounter)`**: Calls `updateCounter` again for the next frame, creating a smooth animation.
    - **`if (progress < 1)`**: Continues the animation until it’s complete.
  - **Analogy**: It’s like a car’s odometer rolling up to a number smoothly instead of jumping instantly.

- **`observer.unobserve(entry.target)`**: Stops watching the section after animating to avoid repeating.

**Why it’s useful**: Makes stats look dynamic and engaging.

**What to ask if confused**:
- What’s `requestAnimationFrame`, and why use it instead of `setInterval`?
- How does `data-target` work in HTML?
- Why unobserve the element?

**Simplified example**:
```javascript
function countUp(element, target) {
    let count = 0;
    const interval = setInterval(() => {
        if (count >= target) {
            clearInterval(interval);
        }
        element.textContent = count;
        count++;
    }, 20);
}
countUp(document.querySelector('.number'), 100);
```

---

### **8. `debounce` Utility Function**

```javascript
function debounce(func, delay = 100) {
    let timeout;
    return (...args) => {
        clearTimeout(timeout);
        timeout = setTimeout(() => func(...args), delay);
    };
}
```

**What it does**: Limits how often a function (like `handleScroll`) runs to improve performance.

- **`function debounce(func, delay = 100)`**: Takes a function (`func`) and a delay (default 100ms).
- **`let timeout`**: Stores a timer ID.
- **`return (...args) => { ... }`**: Returns a new function that wraps the original.
  - **`clearTimeout(timeout)`**: Cancels any previous timer.
  - **`timeout = setTimeout(() => func(...args), delay)`**: Waits `delay` ms before running `func` with its arguments (`...args`).
  - **Analogy**: Imagine you’re typing a search query. Instead of searching after every letter, `debounce` waits until you stop typing for 100ms before searching.

**Why it’s useful**: Prevents `handleScroll` from running too often during scrolling, which could slow down the page.

**What to ask if confused**:
- Why do we need to debounce scroll events?
- What are `...args`?

**Simplified example**:
```javascript
function logMessage() {
    console.log('Function ran!');
}
const debouncedLog = debounce(logMessage, 200);
window.addEventListener('scroll', debouncedLog);
```

---

### **9. `initSidebarToggle()`: Sidebar Animation**

```javascript
function initSidebarToggle() {
    window.addEventListener('scroll', () => {
        const sidebarItems = document.querySelectorAll('.sidebar-item');
        sidebarItems.forEach((item, index) => {
            setTimeout(() => {
                item.classList.toggle('visible', window.scrollY > 100);
            }, index * 100);
        });
    });
}
```

**What it does**: Shows or hides sidebar items (like social media icons) with a staggered animation when scrolling past 100 pixels.

- **`window.addEventListener('scroll', () => { ... })`**: Runs when the user scrolls.
- **`const sidebarItems = document.querySelectorAll('.sidebar-item')`**: Finds all sidebar items.
- **`sidebarItems.forEach((item, index) => { ... })`**: Loops through each item.
  - **`setTimeout(() => { ... }, index * 100)`**: Delays each item’s animation by 100ms times its index (e.g., first item: 0ms, second: 100ms, etc.).
  - **`item.classList.toggle('visible', window.scrollY > 100)`**: Adds `visible` class if scrolled past 100px, triggering the CSS animation.

**Why it’s useful**: Creates a smooth, staggered appearance for sidebar icons.

**What to ask if confused**:
- Why use `setTimeout` for each item?
- What does `index` do in the loop?

**Simplified example**:
```javascript
window.addEventListener('scroll', () => {
    if (window.scrollY > 50) {
        document.querySelector('.sidebar').classList.add('show');
    } else {
        document.querySelector('.sidebar').classList.remove('show');
    }
});
```

---

### **10. `certifications()`: Certification Carousel**

This is a complex function, so I’ll break it down carefully.

```javascript
function certifications() {
    const carousel = document.querySelector('.carousel-track');
    const prevBtn = document.getElementById('prev-btn');
    const nextBtn = document.getElementById('next-btn');
    const viewAllBtn = document.getElementById('view-all-certifications');
    const modal = document.getElementById('certifications-modal');
    const closeModal = document.querySelector('.close-modal');

    // Certification section visibility
    const certSection = document.getElementById('certifications');
    certSection.style.opacity = '0';
    certSection.style.transition = 'opacity 0.8s ease';

    function isInViewport(element) {
        const rect = element.getBoundingClientRect();
        return (
            rect.top <= (window.innerHeight || document.documentElement.clientHeight) &&
            rect.bottom >= 0
        );
    }

    function checkScroll() {
        if (isInViewport(certSection) && certSection.style.opacity === '0') {
            certSection.style.opacity = '1';
        }
    }

    checkScroll();
    window.addEventListener('scroll', checkScroll);

    // Carousel navigation
    let scrollAmount = 0;
    const itemWidth = document.querySelector('.certification-item').offsetWidth;
    const totalItems = document.querySelectorAll('.certification-item').length;

    prevBtn.addEventListener('click', function() {
        scrollAmount += itemWidth;
        if (scrollAmount > 0) {
            scrollAmount = -(totalItems / 2 * itemWidth);
        }
        carousel.style.transform = `translateX(${scrollAmount}px)`;
        carousel.style.transition = 'transform 0.5s ease';
        setTimeout(() => {
            carousel.style.transition = '';
            carousel.style.animation = 'none';
            carousel.offsetHeight;
            carousel.style.animation = 'carousel-scroll 40s linear infinite';
        }, 500);
    });

    nextBtn.addEventListener('click', function() {
        scrollAmount -= itemWidth;
        if (scrollAmount < -(totalItems / 2 * itemWidth)) {
            scrollAmount = 0;
        }
        carousel.style.transform = `translateX(${scrollAmount}px)`;
        carousel.style.transition = 'transform 0.5s ease';
        setTimeout(() => {
            carousel.style.transition = '';
            carousel.style.animation = 'none';
            carousel.offsetHeight;
            carousel.style.animation = 'carousel-scroll 40s linear infinite';
        }, 500);
    });

    // Modal functionality
    viewAllBtn.addEventListener('click', function() {
        modal.classList.add('active');
        document.body.style.overflow = 'hidden';
    });

    closeModal.addEventListener('click', function() {
        modal.classList.remove('active');
        document.body.style.overflow = '';
    });

    modal.addEventListener('click', function(event) {
        if (event.target === modal) {
            modal.classList.remove('active');
            document.body.style.overflow = '';
        }
    });

    document.addEventListener('keydown', function(event) {
        if (event.key === 'Escape' && modal.classList.contains('active')) {
            modal.classList.remove('active');
            document.body.style.overflow = '';
        }
    });

    // Touch swipe functionality
    let touchStartX = 0;
    let touchEndX = 0;

    carousel.addEventListener('touchstart', function(event) {
        touchStartX = event.changedTouches[0].screenX;
        carousel.style.animationPlayState = 'paused';
    }, { passive: true });

    carousel.addEventListener('touchend', function(event) {
        touchEndX = event.changedTouches[0].screenX;
        handleSwipe();
        setTimeout(() => {
            carousel.style.animationPlayState = 'running';
        }, 500);
    }, { passive: true });

    function handleSwipe() {
        const swipeThreshold = 50;
        if (touchEndX < touchStartX - swipeThreshold) {
            nextBtn.click();
        }
        if (touchEndX > touchStartX + swipeThreshold) {
            prevBtn.click();
        }
    }

    // Responsive adjustments
    function updateCarouselDisplay() {
        const viewportWidth = window.innerWidth;
        if (viewportWidth < 576) {
            document.querySelectorAll('.certification-item').forEach(item => {
                item.style.width = '180px';
            });
        } else if (viewportWidth < 768) {
            document.querySelectorAll('.certification-item').forEach(item => {
                item.style.width = '200px';
            });
        } else if (viewportWidth < 1200) {
            document.querySelectorAll('.certification-item').forEach(item => {
                item.style.width = '220px';
            });
        } else {
            document.querySelectorAll('.certification-item').forEach(item => {
                item.style.width = '250px';
            });
        }
    }

    updateCarouselDisplay();
    window.addEventListener('resize', updateCarouselDisplay);
}
```

**What it does**: Manages a carousel that scrolls through certifications, with buttons to navigate, a modal to view all certifications, and touch support for mobile devices.

- **Element selection**: Finds the carousel track, navigation buttons, modal, etc.
- **Section visibility**:
  - **`certSection.style.opacity = '0'`**: Hides the certifications section initially.
  - **`isInViewport`**: Checks if the section is visible in the viewport.
  - **`checkScroll`**: Sets `opacity` to 1 when the section is scrolled to.
- **Carousel navigation**:
  - **`scrollAmount`**: Tracks how far the carousel has moved.
  - **`itemWidth`**: Width of one certification item.
  - **`prevBtn`/`nextBtn` listeners**: Move the carousel left or right by one item’s width, with a loop-around effect.
  - **`carousel.offsetHeight`**: Forces a reflow to restart the CSS animation.
- **Modal functionality**:
  - **`viewAllBtn`**: Opens the modal.
  - **`closeModal`**: Closes it.
  - **Click outside or press Escape**: Also closes the modal.
- **Touch swipe**:
  - Tracks touch start/end positions to detect swipes, triggering `prevBtn` or `nextBtn`.
- **Responsive adjustments**:
  - **`updateCarouselDisplay`**: Changes item widths based on screen size.

**Why it’s useful**: Makes certifications interactive and mobile-friendly.

**What to ask if confused**:
- How does the carousel loop work?
- What’s `offsetHeight` doing?
- How does touch swipe detection work?

**Simplified example**:
```javascript
const track = document.querySelector('.track');
const next = document.querySelector('.next');
next.addEventListener('click', () => {
    track.style.transform = 'translateX(-100px)';
});
```

---

### **11. `initializeCertificationDetailModal()`: Certification Details Modal**

This is another complex function, so let’s simplify it.

```javascript
function initializeCertificationDetailModal() {
    const detailModal = document.getElementById('certification-detail-modal');
    const closeDetailModal = detailModal.querySelector('.close-modal');
    const modalImage = document.getElementById('modal-certification-image');
    const modalTitle = document.getElementById('modal-certification-title');
    const modalIssuer = document.getElementById('modal-certification-issuer');
    const modalDate = document.getElementById('modal-certification-date');
    const modalDescription = document.getElementById('modal-certification-description').querySelector('p');
    const modalSkills = document.getElementById('modal-certification-skills');
    const modalValidity = document.getElementById('modal-certification-validity');
    const viewCredentialBtn = document.getElementById('view-credential-btn');

    const certificationDetails = { /* Object with certification data */ };

    const addClickEvents = () => {
        document.querySelectorAll('.certification-content').forEach(certItem => {
            certItem.addEventListener('click', function() {
                const certTitle = this.querySelector('h3').textContent;
                displayCertificationDetails(certTitle);
            });
        });
        document.querySelectorAll('.certification-grid-item').forEach(certItem => {
            certItem.addEventListener('click', function() {
                const certTitle = this.querySelector('h3').textContent;
                const viewAllModal = document.getElementById('certifications-modal');
                viewAllModal.classList.remove('active');
                displayCertificationDetails(certTitle);
            });
        });
    };

    function displayCertificationDetails(certificationTitle) {
        const certData = certificationDetails[certificationTitle];
        if (certData) {
            modalImage.style.backgroundImage = `url('${certData.image}')`;
            modalTitle.textContent = certificationTitle;
            modalIssuer.textContent = certData.issuer;
            modalDate.textContent = certData.date;
            modalDescription.textContent = certData.description;
            modalSkills.innerHTML = '';
            certData.skills.forEach(skill => {
                const li = document.createElement('li');
                li.textContent = skill;
                modalSkills.appendChild(li);
            });
            modalValidity.textContent = `Valid until: ${certData.validity || 'Not specified'}`;
            viewCredentialBtn.onclick = () => window.open(certData.credentialUrl, '_blank');
            detailModal.classList.add('active');
            document.body.style.overflow = 'hidden';
        }
    }

    closeDetailModal.addEventListener('click', () => {
        detailModal.classList.remove('active');
        document.body.style.overflow = '';
    });

    detailModal.addEventListener('click', (event) => {
        if (event.target === detailModal) {
            detailModal.classList.remove('active');
            document.body.style.overflow = '';
        }
    });

    document.addEventListener('keydown', (event) => {
        if (event.key === 'Escape' && detailModal.classList.contains('active')) {
            detailModal.classList.remove('active');
            document.body.style.overflow = '';
        }
    });

    addClickEvents();

    const certificationContainer = document.querySelector('.certifications-container');
    if (certificationContainer) {
        const observer = new MutationObserver(() => addClickEvents());
        observer.observe(certificationContainer, { childList: true, subtree: true });
    }
}
```

**What it does**: Shows a modal with details when a certification is clicked, pulling data from a predefined object.

- **Element selection**: Finds modal elements for displaying details.
- **`certificationDetails`**: An object storing data for each certification (e.g., title, issuer, image).
- **`addClickEvents`**: Adds click listeners to certification items to open the details modal.
- **`displayCertificationDetails`**: Populates the modal with data for the clicked certification.
- **Modal controls**: Closes the modal via button, outside click, or Escape key.
- **Mutation observer**: Watches for new certification items (e.g., added dynamically) and adds click events.

**Why it’s useful**: Provides detailed info about certifications interactively.

**What to ask if confused**:
- How does the `certificationDetails` object work?
- What’s a Mutation Observer?
- Why clear `modalSkills.innerHTML`?

**Simplified example**:
```javascript
const button = document.querySelector('.cert');
const modal = document.querySelector('.modal');
button.addEventListener('click', () => {
    modal.style.display = 'block';
});
```

---

### **Key Takeaways for Beginners**

1. **Event Listeners**: Most of your code uses `addEventListener` to respond to user actions (clicks, scrolls, etc.).
2. **CSS Classes**: You toggle classes (e.g., `visible`, `dark-mode`) to trigger CSS styles or animations.
3. **Intersection Observer**: Used to animate elements when they’re visible, improving performance.
4. **Local Storage**: Saves user preferences (like dark mode) across visits.
5. **Debouncing**: Limits function calls for performance.
6. **Modals and Carousels**: Complex but made up of simple steps (select elements, update styles, handle clicks).

**Next Steps**:
- Experiment with one function at a time (e.g., try changing the `threshold` in `initAnimations`).
- Add console logs (e.g., `console.log('Clicked!')`) to see when events fire.
- Ask specific questions about any part that’s unclear!
