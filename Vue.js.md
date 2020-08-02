### 1.v-show 与 v-if 区别
1. v-hsow和v-if的区别：
v-show是css切换，v-if是完整的销毁和重新创建。
2. 使用
频繁切换时用v-show，运行时较少改变时用v-if
3. v-if=‘false’ v-if是条件渲染，当false的时候不会渲染

### 绑定 class 的数组用法
1. 对象方法 v-bind:class="{'orange': isRipe, 'green': isNotRipe}"
2. 数组方法v-bind:class="[class1, class2]"
3. 行内 v-bind:style="{color: color, fontSize: fontSize+'px' }"
