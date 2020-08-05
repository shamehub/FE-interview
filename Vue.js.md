### 1.v-show 与 v-if 区别
1. v-hsow和v-if的区别：
v-show是css切换，v-if是完整的销毁和重新创建。
2. 使用
频繁切换时用v-show，运行时较少改变时用v-if
3. v-if=‘false’ v-if是条件渲染，当false的时候不会渲染

### 2.绑定 class 的数组用法
1. 对象方法 v-bind:class="{'orange': isRipe, 'green': isNotRipe}"
2. 数组方法v-bind:class="[class1, class2]"
3. 行内 v-bind:style="{color: color, fontSize: fontSize+'px' }"

### 3.计算属性和 watch 的区别
计算属性是自动监听依赖值的变化，从而动态返回内容，监听是一个过程，在监听的值变化时，可以触发一个回调，并做一些事情。
所以区别来源于用法，只是需要动态值，那就用计算属性；需要知道值的改变后执行业务逻辑，才用 watch，用反或混用虽然可行，但都是不正确的用法。
说出一下区别会加分
1. computed 是一个对象时，它有哪些选项？
   - 有get和set两个选项
2. computed 和 methods 有什么区别？
   - methods是一个方法，它可以接受参数，而computed不能，computed是可以缓存的，methods不会。
3. computed 是否能依赖其它组件的数据？
   - computed可以依赖其他computed，甚至是其他组件的data
4. watch 是一个对象时，它有哪些选项？
   - watch 配置
   - handler
   - deep 是否深度
   - immeditate 是否立即执行

总结

当有一些数据需要随着另外一些数据变化时，建议使用computed。
当有一个通用的响应数据变化的时候，要执行一些业务逻辑或异步操作的时候建议使用watcher

### 4.事件修饰符
1. 绑定一个原生的click事件， 加native，
2. 其他事件修饰符
   - .stop
   - .prevent
   - .capture
   - .once
   - .self
3. 组合键:click.ctrl.exact 只有ctrl被按下的时候才触发

### 5.组件中 data 为什么是函数
因为组件是用来复用的，JS 里对象是引用关系，这样作用域没有隔离，而 new Vue 的实例，是不会被复用的，因此不存在引用对象的问题。

组件中的data写成一个函数，数据以函数返回值形式定义，这样每复用一次组件，就会返回一份新的data，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据。而单纯的写成对象形式，就使得所有组件实例共用了一份data，就会造成一个变了全都会变的结果。

### 6.Vue.js 2.x 双向绑定原理
基本上要知道核心的 API 是通过 Object.defineProperty() 来劫持各个属性的 setter / getter，在数据变动时发布消息给订阅者，触发相应的监听回调，这也是为什么 Vue.js 2.x 不支持 IE8 的原因（IE 8 不支持此 API，且无法通过 polyfill 实现）。

### 7. 对于MVVM的理解？
MVVM 是 Model-View-ViewModel 的缩写。

- Model代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑。

- View 代表UI 组件，它负责将数据模型转化成UI 展现出来。

- ViewModel 监听模型数据的改变和控制视图行为、处理用户交互，简单理解就是一个同步View 和 Model的对象，连接Model和View。

在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。

ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

### 8.Vue组件间的参数传递
1. 父组件传给子组件：子组件通过props方法接受数据;
2. 子组件传给父组件：$emit方法传递参数
3. 兄弟组件传值:eventBus，就是创建一个事件中心，相当于中转站，可以用它来传递事件和接收事件。项目比较小时，用这个比较合适。