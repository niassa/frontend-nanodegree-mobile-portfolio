## Front-end Nanodegree Website Optimization Project

This project utilizes lessons learned in the Udacity modules for Web Optimization (https://www.udacity.com/course/ud884). The purpose of this project is to optimize the given site files for speed and efficiency. This includes optimizing the `index.html` page for speed, and the `pizza.html` page for both speed and animation rate \(frames per second animation\).  

Using PageSpeed Insights, I verified the `index.html` page is optimized above the required 90 threshold for both mobile and desktop, and and `pizza.html` meets the requirements for page speed optimization and stays within the 60 fps parameters.

### Using This App
For the section of the project regarding `index.html`:

* To view the PageSpeed information for the `index.html` file, navigate your browser to the [PageSpeed Insights page](https://developers.google.com/speed/pagespeed/insights/) and enter the location of the `index.html` file from GitHub Pages (http://niassa.github.io/frontend-nanodegree-mobile-portfolio-master/index.html).
* Select the **Analyze** button to run the analysis.
* Switch between the **Mobile** and **Desktop** tabs to view the optimization records for their respective counterparts.

For the section of the project regarding `pizza.html` and `main.js`:

* To view the PageSpeed information for the `pizza.html` file, navigate your browser to the [PageSpeed Insights page](https://developers.google.com/speed/pagespeed/insights/) and enter the location of the `pizza.html` file from GitHub Pages (http://niassa.github.io/frontend-nanodegree-mobile-portfolio-master/views/pizza.html).
* Select the **Analyze** button to run the analysis.
* Switch between the **Mobile** and **Desktop** tabs to view the optimization records for their respective counterparts.

### Achieving the Required Optimizations

#### index.html
* The first thing I did was move the Google Analytics script to the end of the document, while also making it load asynchronously by adding the `async` attribute.
* I added the `async` attribute to the `perfmatters.js` script tag, as well.
* Since the css was not extensive, to assist with the CSS performance issues, I minified it and made it inline within the html instead. I also added a `media` attribute to the `print.css` \(which was minified into `print.min.css`\).
* I web optimized the original `pizzeria.jpg` file into various sizes, called using a `srcset` attribute.

#### css/style.css
* I minified the code and chose to inline it directly into `index.html` as it was not very extensive code, thus rendering `style.css` obsolete.

#### css/print.css
* I minified the code and saved it as `print.min.css`, calling it in `index.html` using a `media` attribute. This style is only used when the page is to be printed.

#### views/pizza.html
* Just as with `index.html`, since the css was not extensive, I minified it and made it inline within the html instead.

#### views/js/main.js
This is where the majority of the work performed for this project occurred.
* **changePizzaSizes** function:
  * Removed the `determineDX` function, pulling the `sizeSwitcher` function out and making it its own function
  * Changed the `querySelectorAll` methods to the more efficient `getElementsByClassName` method instead
  * Removed `changeWidth = (sizeSwitcher(size) * 100)` from the `for` loop to prevent it from continually recalculating through every iteration.
* Changed to `var pizzasToDraw = (window.innerHeight / 50) + (window.innerWidth / 50);` to make it more efficient to determine the scroll for the background pizzas.
* **updatePositions** function:
  * Pulled the `items` variable from the function as it only needs to be declared once (before the function runs)
  * Pulled the `scrollTop` variable out of the loop to prevent it from continually running the lookup with each iteration.
  * Changed the `querySelectorAll` methods to the more efficient `getElementsByClassName` methods instead
  * Borrowed an idea from a Udacity forum post \(that I can't seem to find again and forgot to bookmark it!\) that linked to a github repo with information and ideas on leveraging caching in an array
* I then minified the code into a new file \(`main.min.js`\) and called that file in `views/pizza.html` instead of the original `main.js`.
* Moved the `pizzasDiv` variable outside of the for loop as it only needs to be defined once.
* Updated `document.addEventListener('DOMContentLoaded', function()` to correctly calculate the number of required pizzas based on calculating rows.

#### All Images
* I web optimized the images in the `images` folder to reduce their size.