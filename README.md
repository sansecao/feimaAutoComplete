本插件会为你的vscode添加自动补全飞马，setter 各个函数代码的功能，提高开发效率。

## 功能

飞马代码自动补全


## 飞马组件开发 - setter

> setter（设置器）是针对组件属性描述类型提供的输入工具，如一个字符串类似的属性，那它对应的setter就是 InputSetter；一个数字类型的属性，那它对应的setter就是 NumberSetter

为更好的组织右侧属性配置面板，飞马设置器针对同一数据类型分别提供了多种设置器类型，如针对字符串的单行文本 以及 多行文本，针对数字的输入设置器以及滑动设置器等。

### 基础设置器

基础设置器部分主要是常见基础数据类型的设置器，返回比较单一的值

#### 字符串

##### InputSetter

- 描述：单行文本输入

- 配置：无

##### TextAreaSetter

- 描述：多行文本输入

- 配置：无

#### 数字

##### NumberSetter

- 描述：数字输入框

- 配置：
  
  ```javascript
  {
    min: 0,
    max: 100,
    step: 1
  }
  ```

##### SliderSetter

- 描述：滑动输入框

- 配置：
  
  ```javascript
  {
    min: 0,
    max: 100,
    step: 1
  }
  ```

#### 枚举值

##### RadioSetter

- 描述：单选框，所有选项可见（建议可选项在小于等于3个的时候使用）

- 配置：
  
  ```javascript
  {
    size: 'small',
    data: [
      { label: '成功', value: 'success' },
      { label: '信息', value: 'info' },
      { label: '警告', value: 'warning' },
    ]
  }
  ```

##### SelectSetter

- 描述：下拉框（作用与RadioSetter一致，对更多项的选项兼容性更好）

- 配置：
  
  ```javascript
  {
    size: 'small',
    data: [
      { label: '成功', value: 'success' },
      { label: '信息', value: 'info' },
      { label: '警告', value: 'warning' },
    ]
  }
  ```

#### 布尔值 SwitchSetter

- 描述：antd 开关样式设置器，值为true/false

- 配置：无、

#### 颜色 ColorSetter

- 描述：颜色选择输入

- 配置：无

#### 日期时间 DateTimeSetter

- 描述：日期时间设置器，用于设置一个日期 或者 时间的字符串值

- 配置
  
  ```javascript
  {
    type: 'dateTime', // dateTime || date || time, default dateTime
    format: 'YYYY-MM-DD HH:mm:ss' // dafault YYYY-MM-DD HH:mm:ss
  }
  ```

### 高级设置器

高级设置器是飞马提供的复合设置器，用以完成一些比较复杂的属性配置，如数组、函数等

#### 函数表达式 EditorSetter

- 描述：生成一个编辑器按钮，点击后可以唤出代码编辑器，最终返回一个JS合法值或者函数

- 配置
  
  ```javascript
  const DEFAULT_AFTER_FETCH = `
  function(res) {
    console.log('res', res);
  }
  `;
  {
    label: '编辑', // 按钮标签
    type: 'JSExpression', // 编辑器类型：JSExpression(表达式) || JSFunction(函数)， default JSExpression
    defaultValue: DEFAULT_AFTER_FETCH, // 初始化编辑器内容，非必须
  }
  ```

#### 事件 EventSetter

- 描述：生成一个事件设置器，接收事件名，生成一系列事件函数体（可以由EditorSetter代替）

- 配置
  
  ```javascript
  const DEFAULT_FUNCTION_ONCANCEL = `
  function(res) {
    console.log('res', res);
  }
  `;
  const DEFAULT_FUNCTION_ONOK = `
  function(res) {
    console.log('res', res);
  }
  `;
  [
    {
      label: '当取消时',
      name: 'onCancel',
      initialValue: DEFAULT_FUNCTION_ONCANCEL,
    },
    {
      label: '当确认时',
      name: 'onOk',
      initialValue: DEFAULT_FUNCTION_ONOK,
    },
  ]
  ```

#### 表单校验规则 FormValidationSetter

- 描述：antd 表单项的校验规则设置器，返回一个标准的antd formItem rule

- 配置：无

#### 请求 RemoteSetter

- 描述：生成一个标准的飞马请求配置对象，组件中用来接收一个请求配置

- 配置
  
  ```javascript
  {
    remoteNamePrefix: '', // 请求配置的属性名（若不配置，则会打平后透传给组件，组件属性上会接收到 __remote, __dateType, __variable）
    // 此处的默认数据以及默认函数仅作为用户编辑属性时的初始化展示，并不会实际回传给组件，只有用户真正编辑了内容后，才会回传，所以并非是默认值的功能
    variableInitialValue: '', // 静态数据的初始值
    onlyRemote: false, // 是否仅允许请求配置
    defaultBeforeFetch: '', // 默认请求拦截函数
    defaultAfterFetch: '', // 默认请求响应拦截函数
    variable: {
      // 一个完整的 setter 配置，用于静态变量的配置覆盖
    }
  }
  ```

#### 数组 ArraySetter

- 描述：生成数组数据设置器，提供对数组的增、删、改以及排序等基础标准操作

- 配置
  
  ```javascript
  {
    subPropConf: [
      {
        // 完整的属性配置对象
        name: 'title',
        title: '列名',
        useExp: true,
        initialValue: '姓名',
        setter: 'InputSetter',
      }
    ],
    nameArr: ['title'], // 展示到右侧面板的属性配置名
  }
  ```

## 反馈/帮助更正BUG

本插件代码开源，欢迎大家更正bug或添加其他实用功能！

**Enjoy!**
