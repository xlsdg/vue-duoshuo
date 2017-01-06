<template>
  <div class="ds-thread"
    :data-thread-key="thread"
    :data-title="title"
    :data-url="url"
    :data-author-key="author"
  ></div>
</template>

<style scoped>
  .ds-thread {
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
      url: {
        type: String,
        required: false,
        default: window.location.href
      },
      title: {
        type: String,
        required: false,
        default: window.document.title
      },
      author: {
        type: String,
        required: false
      }
    },
    data() {
      return {
        dom: null
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

        if (!window.DUOSHUO) {
          const ds = document.createElement('script');
          ds.type = 'text/javascript';
          ds.async = true;
          ds.charset = 'UTF-8';
          if (ds.readyState) {
            ds.onreadystatechange = function() {
              if (ds.readyState === 'loaded' || ds.readyState === 'complete') {
                ds.onreadystatechange = null;
                that.ready();
              }
            };
          } else {
            ds.onload = function() {
              ds.onload = null;
              that.ready();
            };
          }
          ds.src = `//static.duoshuo.com/embed.js?_t=${(new Date()).getTime()}`;
          that.dom = ds;
          const s = document.getElementsByTagName('script')[0];
          s.parentNode.insertBefore(ds, s);
        }
      },
      ready() {
        const that = this;
        that.$nextTick(function() {
          if (window.DUOSHUO && window.DUOSHUO.EmbedThread) {
            that.$emit('ready', null);
            window.DUOSHUO.EmbedThread(that.$el);
          }
        });
      },
      destroy() {
        const that = this;
        // that.dom.parentNode.removeChild(that.dom);
        that.dom = null;
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
      const that = this;
      // console.log('mounted');
      that.ready();
    },
    beforeUpdate() {
      // const that = this;
      // console.log('beforeUpdate');
    },
    updated() {
      // const that = this;
      // console.log('updated');
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
