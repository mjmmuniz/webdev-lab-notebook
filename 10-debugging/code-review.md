## Code Review Exercise

Write your code review here in markdown format.

## Issue #1 & 2: Usability & Accuracy

In the Cat Facts section, when the "Load New Cat Facts" button was pressed, the cat facts actually just disappeared, no new facts appeared, there was no loading icon, and there was no error message. This is an issue as the feature is not working as expected. I edited the JavaScript code to set the loadingContainer attribute to a class named loading-container and the loading attribute to both the loading-container and display-none class. Now, cat facts would appear but they were the same first 10 every time. To address this, I added a randNum variable to pick a random page in the API to get 10 cat facts from, not just the same first one each time.

Initial code:

```
const createLoadingContainer = function () {
const loadingContainer = document.querySelector('.loading-container');
const loader = document.createElement('img');
loader.src = '../../images/loader.gif';
loader.alt = 'loader gif while the data loads';
loader.width = 60;
loader.height = 60;
loadingContainer.append(loader);
};

const fetchCatFacts = async function () {
const catFactsList = document.getElementById('cat-facts-list');
catFactsList.replaceChildren();

createLoadingContainer();

try {
const response = await fetch('https://catfact.ninja/facts?limit=10');
const data = await response.json();

    data.data.forEach((element) => {
      const catFactItem = document.createElement('p');
      catFactItem.setAttribute('class', 'cat-fact-list-item');
      catFactItem.textContent = element.fact;
      catFactsList.append(catFactItem);
    });

} catch (error) {
console.error('Error fetching cat facts:', error);
} finally {
const loading = document.querySelector('.loading-container');
loading.setAttribute('class', 'display-none');
}
};
```

Updated code:

```
const createLoadingContainer = function () {
const loadingContainer = document.querySelector(".loading-container");
loadingContainer.replaceChildren();
loadingContainer.setAttribute("class", "loading-container");

const loader = document.createElement("img");
loader.src = "../../images/loader.gif";
loader.alt = "loader gif while the data loads";
loader.width = 60;
loader.height = 60;
loadingContainer.append(loader);
};

const fetchCatFacts = async function () {
const catFactsList = document.getElementById("cat-facts-list");
catFactsList.replaceChildren();

createLoadingContainer();

try {
const randNum = Math.floor(Math.random() \* 15) + 1;
const response = await fetch(
`https://catfact.ninja/facts?limit=10&page=${randNum}`,
);
const data = await response.json();

    data.data.forEach((element) => {
      const catFactItem = document.createElement("p");
      catFactItem.setAttribute("class", "cat-fact-list-item");
      catFactItem.textContent = element.fact;
      catFactsList.append(catFactItem);
    });

} catch (error) {
console.error("Error fetching cat facts:", error);
} finally {
const loading = document.querySelector(".loading-container");
loading.setAttribute("class", "loading-container display-none");
}
};
```

## Issue #3: Responsiveness

In the Request Info section, when pressing either the "submit" button or the "reset" button, nothing happened. This is a problem as the user cannot properly submit the form to learn new information or clear the form to restart. To fix this, I just moved the closing </form> tag to after the buttons in the HTML code so both buttons were now apart of the form.

Initial code:

```
        <label class="form-label" for="message"
          >Feel free to leave a message to us</label
        >
        <textarea
          class="form-textarea form-element-container"
          name="message"
          id="message"
          cols="30"
          rows="10"
        ></textarea>
        </form>
        <div
          class="form space-evenly-distributed-row-container form-buttons-container"
        >
          <input class="form-button" type="submit" value="submit" />
          <input class="form-button" type="reset" value="reset" />
        </div>
    </div>
```

Updated code:

```
        <label class="form-label" for="message"
          >Feel free to leave a message to us</label
        >
        <textarea
          class="form-textarea form-element-container"
          name="message"
          id="message"
          cols="30"
          rows="10"
        ></textarea>
        <div
          class="form space-evenly-distributed-row-container form-buttons-container"
        >
          <input class="form-button" type="submit" value="submit" />
          <input class="form-button" type="reset" value="reset" />
        </div>
      </form>
    </div>
```
