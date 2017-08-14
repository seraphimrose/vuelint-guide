# vuelint-guide

[JSX-styled can refer to the React guide]

## 使用单文件组件 (single-file-components)

```html
<template>
  <div>This is ok</div>
</template>

<script>
export default {

}
</script>
```

## 采用自闭合风格的标签 (self-closed)

```html
<!-- Bad -->
<component></component>

<!-- Bad -->
<component>

<!-- Bad -->
<component/>

<!-- Good -->
<component />
```

## 模板内组件名和属性使用短横线风格 (kebab-case)

```html
<!-- Bad -->
<MyComponent myProps="foo" />

<!-- Good -->
<my-component my-props="foo" />
```

## 多属性标签风格 (multi-props-tag-styles)

```html
<!-- bad -->
<component foo="a" bar="b"/>

<!-- bad -->
<component foo="a"
  bar="b" />

<!-- ok -->
<component foo="a" bar="b" />

<!-- ok -->
<component
  foo="a"
  bar="b"
/>

<!-- best -->
<component
  foo="a"
  bar="b" />

<!-- bad -->
<component
  foo="a"
  bar="b">text
</component>

<!-- bad -->
<component
  foo="a"
  bar="b">
text</component>

<!-- ok -->
<component
  foo="a"
  bar="b"
>text</component>

<!-- ok -->
<component
  foo="a"
  bar="b"
>
  text
</component>

<!-- best -->
<component
  foo="a"
  bar="b">
  text
</component>
```

## 模板绑定的 {{ }} 前后都应该有空格 (space-before-brackets)
```html
<!-- Bad -->
<div>{{data}}</div>

<!-- Good -->
<div>{{ data }}</div>
```

## 不使用js的字符串模板拼接动态数据 (no-js-template)
```html
<!-- Bad -->
<component>
  {{ `pay for ${price}` }}
</component>

<!-- Good -->
<component>
  pay for {{ price }}
</component>
```

## v-for属性 (v-for)
```html
<!-- Bad -->
<component v-for="item in list" />

<!-- Bad -->
<component
  v-for="item in list"
  v-if="showList" />

<!-- Good -->
<template v-if="showList">
  <component
    v-for="item in list"
    :key="item.id" />
</template>
```

## 属性顺序 (order of props in tags)
```html
<!-- recommended -->
<!-- '|' means you can only use one of them -->
<!-- '/' means you can order them as you like -->
<component
  v-for | v-if | v-else
  @click
  key
  ref
  v-*
  class / style
  value-props / handler-props
/>

```

## 不宜直接将整个对象传入组件 (simple-props)
```html
<!-- Bad -->
<component :obj="obj" />

<!-- Good -->
<component
  :id="obj.id"
  :name="obj.name"
  :value="obj.value" />
```

## 给组件的属性赋予初始值 (props-default-value)
```html
<template>
  <div>Hello, {{ name }}</div>
</template>
<script>
export default {
  props: {
    name: {
      type: String,
      default() { return 'Guest' },
    },
  },
}

</script>
```

## 尽量避免使用this.$refs与this.$parent实现组件通信 (avoid-refs-and-parent)

```javascript
// bad
export default {
  methods: {
    this.$refs.modal.open()
  },
}
```


## 组件内属性的顺序 (props-order-in-components)
```javascript
// just recommend
export default {
  name: 'Component',

  props: {},
  mixins: {},
  extends: {},

  components: {},

  data() {},
  computed: {},
  filters: {},

  methods: {},
  watch: {},

  mounted() {},
  destroyed() {},
}


// and you can put some lifecycle hooks before the 'data', because of logical reasons, like:
export default {
  mounted() {},
  // because we are extremely concerned about what the component will do when mounted

  data() {},
  computed: {},

  destroyed() {},
}

```

## 不在模板中引入复杂逻辑 (simple logic in template)
```html
<!-- Bad -->
<template>
  <div>
    Time is {{ hour }}:{{ minute }}:{{ second }}
  </div>
</template>

<!-- Good -->
<template>
  <div>
    Time is {{ time }}
  </div>
</template>

<script>
export default {
  computed: {
    time() {
      return `${hour}:${minute}:${second}`
    },
  },
}
</script>
```

## 不要混用 filter、computed、methods (good-use-of-fcm)
```javascript
// filter: The data is ready to show, but it won't be shown to UI by raw, may be formatted.

// computed: Computing data for avoiding describing complex logic repeatedly (especially complex logic in template).

// methods: Other functions and handlers, and params-needed 'computed'.
```
