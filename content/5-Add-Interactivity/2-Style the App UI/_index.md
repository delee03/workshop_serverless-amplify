+++
title = "Style the App UI"
date = 2024
weight = 2
chapter = false
pre = "<b>6.2. </b>"
+++

On your local machine, navigate to the profilesapp/src/index.css file and update it with the following code. Then, save the file.

![Update Index.CSS](/images/workshop-setup/5_indexCSS.png?width=full)

```css
:root {
    font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
    line-height: 1.5;
    font-weight: 400;

    color: rgba(255, 255, 255, 0.87);

    font-synthesis: none;
    text-rendering: optimizeLegibility;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;

    max-width: 1280px;
    margin: 0 auto;
    padding: 2rem;
}

.card {
    padding: 2em;
}

.read-the-docs {
    color: #888;
}

.box:nth-child(3n + 1) {
    grid-column: 1;
}
.box:nth-child(3n + 2) {
    grid-column: 2;
}
.box:nth-child(3n + 3) {
    grid-column: 3;
}
```
