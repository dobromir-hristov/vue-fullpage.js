# Vue-fullpage.js
![preview](https://alvarotrigo.com/fullPage/vue-fullpage/imgs/vue-fullpage-wrapper.png)
<p align="center">
Official Vue.js wrapper for the <a target="_blank" href="https://github.com/alvarotrigo/fullPage.js/">fullpage.js library</a>.
</p>

- [Demo online](https://alvarotrigo.com/vue-fullpage/) | [Codepen](https://codepen.io/alvarotrigo/pen/zpQmwq)
- [fullpage.js Extensions](https://alvarotrigo.com/fullPage/extensions/)
- By [@imac2](https://twitter.com/imac2). Thanks to [VasiliyGryaznoy](https://github.com/VasiliyGryaznoy) , [dragg](https://github.com/dragg) and

## Table of contents
1. [Installation](#installation)
2. [License](#license)
3. [Usage](#usage)
3. [Options](#options)
4. [Methods](#methods)
5. [Callbacks](#callbacks)
6. [Contributing](#contributing)
7. [Resources](#resources)


## Installation
For using of this component you need to include:
- [fullPage.js library](https://github.com/alvarotrigo/fullPage.js/) with **its dependencies** (jQuery)
- Install and register this wrapper like simple Vue.js component.
- Include fullPage.js files (`jquery.fullpage.js` and `jquery.fullpage.css`)


Terminal:
```shell
// With bower
bower install vue-fullpage.js

// With npm
npm install --save vue-fullpage.js
```

Check out [the license](#license) for commercial projects.

## License

### Commercial license
Although vue-fullpage.js is under the MIT license as can be seen on the [LICENSE file](https://github.com/alvarotrigo/vue-fullpage.js/blob/master/LICENSE), notice [fullPage.js library](https://github.com/alvarotrigo/fullPage.js) is under GPLv3. Therefore you'll need to purchase a Commercial License for fullPage.js if you want to use fullPage to develop commercial sites, themes, projects, and applications. [[Purchase a Fullpage Commercial License]](https://alvarotrigo.com/fullPage/pricing/)

### Open source license
If you are creating an open source application under a license compatible with the [GNU GPL license v3](https://www.gnu.org/licenses/gpl-3.0.html), you may use fullPage under the terms of the GPLv3.

**The credit comments in the JavaScript and CSS files should be kept intact** (even after combination or minification)

[Read more about fullPage's license](https://alvarotrigo.com/fullPage/pricing/).

## Usage

### Bundler (Webpack, Rollup)

```js
import Vue from 'vue'
import Vue wrapper for fullpage.js from 'vue-fullpage'
// You need a specific loader for CSS files like https://github.com/webpack/css-loader
import 'vue-fullpage/dist/vue-fullpage.css'

Vue.use(Vue wrapper for fullpage.js)
```

### Browser

```html
<!-- Include after Vue -->
<!-- Local files -->
<link rel="stylesheet" href="vue-fullpage/dist/vue-fullpage.css"></link>
<script src="vue-fullpage/dist/vue-fullpage.js"></script>

<!-- From CDN -->
<link rel="stylesheet" href="https://unpkg.com/vue-fullpage/dist/vue-fullpage.css"></link>
<script src="https://unpkg.com/vue-fullpage"></script>
```

## Required HTML
This wrapper creates a `<full-page>` component , which you can use like other Vue.js components. For example:

```html
<div>
    <full-page ref="fullpage" :options="options" id="fullpage">
    <div class="section">
      First section ...
    </div>
    <div class="section">
      Second section ...
    </div>
  </full-page>
</div>
```

## Options
You can use any [options](https://github.com/alvarotrigo/fullPage.js#options) supported by fullPage.js library.
Just pass options object into this wrapper like Vue.js property. You can see this in the example above.
Options object can contain simple [options](https://github.com/alvarotrigo/fullPage.js#options) as well as fullPage.js [callbacks](https://github.com/alvarotrigo/fullPage.js#callbacks).

## Methods
fullPage.js contains many [methods](https://github.com/alvarotrigo/fullPage.js#methods).
You can use any of them.

Example:
```html
<template>
  <div>
    <full-page ref="fullpage" :options="options">
      <div class="section">
        <button class="next" @click="moveSectionDown">Next</button>
        Section 1
      </div>
      <div class="section">
        <button class="prev" @click="moveSectionUp">Prev</button>
        Section 2
      </div>
    </full-page>
  </div>
</template>
```

Similar you can call any method of fullPage.js library directly on Javascript:

```
fullpage_api.moveSectionDown();
```

## Callbacks
As mentioned [above](#options) you can pass callbacks through options object:
```html
<template>
  <div>
    <full-page ref="fullpage" :options="options">
      <div class="section">
        First section ...
      </div>
      <div class="section">
        Second section ...
      </div>
    </full-page>
  </div>
</template>

<script>
  export default {
      data() {
        return {
          options: {
            afterLoad: this.afterLoad,
          }
        }
      },

      methods: {
        afterLoad() {
          console.log("Emitted 'after load' event.");
        }
      }
    }
</script>
```

Or you can use the standard approach for event handling of Vue.js:
```html
<template>
  <div>
    <full-page @after-load="afterLoad">
        ....
    </full-page>
  </div>
</template>
<script>
  export default {
      methods: {
        afterLoad() {
          ...
        }
      }
    }
</script>

```

Similar you can handle any [event](https://github.com/alvarotrigo/fullPage.js#callbacks) of fullPage.js library.
Just translate camelCase name of callback to kebab-case and use it ;)

## Dynamic changes
vue-fullpage.js will watch all changes taking place within the fullpage.js options but will NOT automatically watch any DOM changes. If you want vue-fullpage.js to react to DOM changes call `$.fn.fullpage.update();` after making those changes. For example:

```javascript
//creating the section div
var section = document.createElement('div');
section.className = 'section';
section.innerHTML = '<h3>New Section</h3>';

//adding section
document.querySelector('#fullpage').appendChild(section);

//where --> var vm = new Vue({...}) if calling it from outside.
vm.$refs.fullpage.build();

//or, when calling it from inside the Vue component methods:
this.$refs.fullpage.build();
```

In order for fullPage.js to get updated after a change in any of the fullPage.js options, you'll have to make sure to use such option in the initialisation.

For example, if we want fullPage.js to get updated whenever I change the `scrollBar` and `controlArrows` options, I'll have to use the following initialisation:

```html
<script>
  export default {
    data() {
      return {
        options: {
          controlArrows: true,
          scrollBar: true
        },
      }
    },
  }
</script>
```

Or, if using `new Vue`, use an object instead of a function for the `data` property:
```javascript
new Vue({
    el: '#app',
    data: {
        options: {
            controlArrows: true,
            scrollBar: true
        },
    }
});
```

## Contributing
Please see [Contributing to fullpage.js](https://github.com/alvarotrigo/fullPage.js/wiki/Contributing-to-fullpage.js)

# Resources
- [Wordpress theme](https://alvarotrigo.com/fullPage/utils/wordpress.html)
- [fullpage.js Extensions](https://alvarotrigo.com/fullPage/extensions/)
- [CSS Easing Animation Tool - Matthew Lein](http://matthewlein.com/ceaser/) (useful to define the `easingcss3` value)
- [fullPage.js jsDelivr CDN](http://www.jsdelivr.com/#!jquery.fullpage)