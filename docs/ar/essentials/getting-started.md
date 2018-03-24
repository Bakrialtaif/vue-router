# البداية 

>  &#x202b;
> مرحباً، سنقوم بإستخدام  [ES2015](https://github.com/lukehoban/es6features) في نماذج الشفرة البرمجية في هذا الدليل.

&#x202b; إنشاء تطبيق من صفحة واحدة SPA بإستخدام vue-Router عملية في غاية البساطة. لأنه بتضمين Vue.js فإننا سلفاً قمنا بتضمين معظم المكونات المطلوبة، بعد إضافة vue-router فإن كل الذي نحتاجه هو إخبار vue أين تجد المكونات التي ستقوم بعمل تفسير render لها وذلك من خلال ضبط المسارات routes التي تؤشر لأمكنة تلك المكونات components.

> &#x202b; كل الأمثلة ستقوم بإستخدام النسخه الكاملة من vue لضمان ترجمة parsing القوالب template بشكل صحيح. تفاصيل أكثر عبر الرابط [هنا](https://vuejs.org/v2/guide/installation.html#Runtime-Compiler-vs-Runtime-only).

### HTML

``` html
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>

<div id="app">
  <h1>Hello App!</h1>
  <p>
    <!-- use router-link component for navigation. -->
    <!-- specify the link by passing the `to` prop. -->
    <!-- `<router-link>` will be rendered as an `<a>` tag by default -->
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>
  </p>
  <!-- route outlet -->
  <!-- component matched by the route will render here -->
  <router-view></router-view>
</div>
```

### JavaScript

``` js
// 0. If using a module system (e.g. via vue-cli), import Vue and VueRouter
// and then call `Vue.use(VueRouter)`.

// 1. Define route components.
// These can be imported from other files
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }

// 2. Define some routes
// Each route should map to a component. The "component" can
// either be an actual component constructor created via
// `Vue.extend()`, or just a component options object.
// We'll talk about nested routes later.
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]

// 3. Create the router instance and pass the `routes` option
// You can pass in additional options here, but let's
// keep it simple for now.
const router = new VueRouter({
  routes // short for `routes: routes`
})

// 4. Create and mount the root instance.
// Make sure to inject the router with the router option to make the
// whole app router-aware.
const app = new Vue({
  router
}).$mount('#app')

// Now the app has started!
```

&#x202b; بحقن المسار يمكننا الوصول إليه وإستخدامه بهذه الطريقة `this.$router`، وعليه فالمسار الحالي هو `this.$route` بداخل أي مكون component 


```js
// Home.vue
export default {
  computed: {
    username () {
      // We will see what `params` is shortly
      return this.$route.params.username
    }
  },
  methods: {
    goBack () {
      window.history.length > 1
        ? this.$router.go(-1)
        : this.$router.push('/')
    }
  }
}
```

&#x202b; خلال هذه الوثائق سنستخدم أحياناً المعرف `router`. تذكر أن `this.$router` هو نفسه `router`. السبب في كوننا نستخدم `this.$router` لأننا لا نريد أن نعيد إستيراد الrouter في كل مكون component.

&#x202b; قم بأخذ لمحه سريعة بهذه المثال [هنا](https://jsfiddle.net/yyx990803/xgrjzsup/).

&#x202b; لاحظ أن `<router-link>` يتحول لحظياً إلى  `.router-link-active` بناءاً على مطابقته مع المسار الحالي الذي قام المستخدم بزيارته، تفاصيل أكثرها من خلال  [API reference](../api/router-link.md).
