# drag-test

Proof of concept that a drag and drop list wouldn't be too difficult to implement in-house.

TODO:
- Customizable drag shadow
  - Since this uses the draggable browser API, the shadow is transparent and that's not customizable. Using the draggable API offers an abstraction that makes the code relatively simple (no calculations involved). To keep this, we can probably import a draggable polyfill.
- Add an item as a child to a child-less parent
- Style:
	- nested borders have to extend full width
	- The borders are currently droppable areas, and hence must take space. Remove from inline to float on-top of items so that they don't create space between the items. 

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
