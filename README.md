# An input and textarea component for Vue.js 2

## Demo

A live demo is available [here](https://dany68.github.io/elements/docs/components/forms#input).

## Installation

You can install the package via npm:

```php
npm install dany68/v-input --save
```

Then you will need to register the component globally in you main js file.

```js
// If Vue has been added to the global scope as:
// window.Vue = require('Vue')
require('v-input');

// Otherwise
import Input from 'v-input';
Vue.use(Input);
```

Alternatively you can register v-input locally:

```js
//in your Component.vue or similar file
import Input from 'v-input';

export default {
    components: { 'v-input': Input }
}
```

## Usage

On your page you can now use html like this to render the input field:

```html
<v-input v-model="name" label="Pseudo" :feedback="{ type: 'success', text: 'This pseudo is amazing.' }"></v-input>
```

The value is synchronized with the `v-model` attribute.

#### Options

| Prop        | Type   | Default | Required | Description                     |
| ----------- |:------:|:-------:|:--------:|:-------------------------------:|
| type        | String | text    | No       | The HTML input type             |
| label       | String |         | No       | Add a floating label            |
| icon        | String |         | No       | Name of the icon to display     |
| placeholder | String |         | No       | The input placeholder           |
| feedback    | Object |         | No       | See the feedback section below  |

## Textarea

To render a textarea instead of an input, set the type option to `textarea`.
If you want to resize the height of the textarea automatically based on the content height add the `autoresize="true"` prop attribute.

## Feedback

The feedback prop is useful to render a validation message and style the input accordingly.
```js
{
    type: 'error',
    text: 'This pseudo already exists' // Optional
}
```

## Addon Slots

You can add left and right addons to the input.
It's useful if you want to display a button, a select dropdown, or whatever you want in either side of the input.

```html
<v-input v-model="search">
    <v-select slot="leftAddon" v-model="filter" :options="['news', 'users']"></v-select>
    <button slot="rightAddon" class="btn">Search</button>
</v-input>
```

## Notes

This package doesn't include CSS styles.
You can either use the [Elements CSS framework](https://github.com/dany68/elements) or simply grab the [input scss file](https://github.com/dany68/elements/tree/master/sass/form/input.scss) from it.
