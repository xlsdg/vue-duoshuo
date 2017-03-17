<template>
  <div class="i-duo-shuo"
    :key="thread"
  ></div>
</template>

<style scoped>
  .i-duo-shuo {
    width: 100%;
    height: 100%;
  }
</style>

<script>
  export default {
    name: 'DuoShuo',
    props: {
      domain: {
        type: String,
        required: true
      },
      thread: {
        type: String,
        required: true
      },
      image: {
        type: String,
        required: false
      },
      author: {
        type: String,
        required: false
      },
      position: {
        type: String,
        required: false
      },
      limit: {
        type: Number,
        required: false
      },
      order: {
        type: String,
        required: false
      }
    },
    data() {
      return {
        dom: null,
        script: null
      };
    },
    computed: {
    },
    watch: {
    },
    methods: {
      init() {
        const that = this;

        if (!window.duoshuoQuery || !window.duoshuoQuery.short_name) {
          window.duoshuoQuery = {
            short_name: that.domain
          };
        } else if (window.duoshuoQuery.short_name !== that.domain) {
          window.duoshuoQuery.short_name = that.domain;
        }

        if (window.DUOSHUO) {
          return that.ready(true);
        }

        const ds = document.createElement('script');
        ds.type = 'text/javascript';
        ds.async = true;
        ds.charset = 'utf-8';
        if (ds.readyState) {
          ds.onreadystatechange = function() {
            if (ds.readyState === 'loaded' || ds.readyState === 'complete') {
              ds.onreadystatechange = null;
              that.ready(false);
            }
          };
        } else {
          ds.onload = function() {
            ds.onload = null;
            that.ready(false);
          };
        }
        ds.src = `${document.location.protocol}//static.duoshuo.com/embed.js?_t=${(new Date()).getTime()}`;
        that.script = ds;
        const s = document.getElementsByTagName('script')[0];
        s.parentNode.insertBefore(ds, s);
      },
      ready(isForceUpdate) {
        const that = this;
        if (window.DUOSHUO && window.DUOSHUO.EmbedThread) {
          if (that.dom) {
            that.dom.parentNode.removeChild(that.dom);
            that.dom = null;
          }
          that.$nextTick(function() {
            const container = window.document.createElement('div');
            container.className = 'ds-thread';
            container.setAttribute('data-thread-key', that.thread);
            container.setAttribute('data-title', window.document.title);
            container.setAttribute('data-url', window.location.href);
            that.author && container.setAttribute('data-author-key', that.author);
            that.image && container.setAttribute('data-image', that.image);
            that.position && container.setAttribute('data-form-position', that.position);
            that.limit && container.setAttribute('data-limit', that.limit);
            that.order && container.setAttribute('data-order', that.order);
            if (isForceUpdate) {
              window.DUOSHUO.EmbedThread(container);
            }
            that.$el.append(container);
            that.dom = container;
            that.$emit('ready', null);
          });
        }
      },
      destroy() {
        const that = this;
        // that.script.parentNode.removeChild(that.script);
        that.script = null;
      }
    },
    beforeCreate() {
      // const that = this;
      // console.log('beforeCreate');
    },
    created() {
      const that = this;
      // console.log('created');
      that.init();
    },
    beforeMount() {
      // const that = this;
      // console.log('beforeMount');
    },
    mounted() {
      // const that = this;
      // console.log('mounted');
    },
    beforeUpdate() {
      // const that = this;
      // console.log('beforeUpdate');
    },
    updated() {
      const that = this;
      // console.log('updated');
      that.ready(true);
    },
    activated() {
      // const that = this;
      // console.log('activated');
    },
    deactivated() {
      // const that = this;
      // console.log('deactivated');
    },
    beforeDestroy() {
      const that = this;
      // console.log('beforeDestroy');
      that.destroy();
    },
    destroyed() {
      // const that = this;
      // console.log('destroyed');
    }
  };
</script>
