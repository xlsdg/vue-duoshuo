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

  Required; 文章在原站点中的 ID 或其他唯一标识

* `image` **[String]**

  Optional; 文章图片地址，将用于转发时的附图

* `author` **[String]**

  Optional; 作者在本站中的 ID

* `position` **[String]**

  Optional; 该页面中评论框的位置，取值 `top` (评论框在顶端显示)，`bottom` (评论框在底端显示)

* `limit` **[Number]**

  Optional; 单页显示评论数，取值范围: 1～200

* `order` **[String]**

  Optional; 排序方式，取值：`asc` (从旧到新)，`desc` (从新到旧)

See more [DuoShuo](http://dev.duoshuo.com/docs/5003ecd94cab3e7250000008)


## Development

``` bash
$ git clone https://github.com/xlsdg/vue-duoshuo.git vue-duoshuo
$ cd vue-duoshuo && npm i && npm run dev
```

Then open `http://localhost:8080/` to see the demo.

# License

MIT
