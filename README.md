# vue-duoshuo

> Vue.js(v2.x+) component wrap for DuoShuo.js

## Installation

``` bash
$ npm install --save vue-duoshuo
```


## Usage

``` vue
<template>
  <div class="duo-shuo">
    <duo-shuo
      domain="test"
      thread="50b344447f32d30066000147"
    ></duo-shuo>
  </div>
</template>

<script type="text/babel">
  import DuoShuo from 'vue-duoshuo';

  export default {
    name: 'view',
    components: {
      DuoShuo
    },
    data() {
      return {
      };
    },
    methods: {
    }
  };
</script>

<style scoped>
  .duo-shuo {
  }
</style>
```

## Properties

* `domain` **[String]**

  Required; DuoShuo short_name 多说二级域名

* `thread` **[String]**

  Required; 文章 ID

* `url` **[String]**

  Optional; `window.location.href` by defualt.

* `title` **[String]**

  Optional; `window.document.title` by defualt.

* `author` **[String]**

  Optional; 作者用户 ID

See more [DuoShuo](http://dev.duoshuo.com/docs/50b344447f32d30066000147)


## Development

``` bash
$ git clone https://github.com/xlsdg/vue-duoshuo.git vue-duoshuo
$ cd vue-duoshuo && npm i && npm run dev
```

Then open `http://localhost:8080/` to see the demo.

# License

MIT
