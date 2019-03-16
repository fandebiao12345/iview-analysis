# Scroll
## scroll组件

在容器上定义了鼠标滚轮运动的事件和容器的滚动事件
``` html
        <div
            :class="scrollContainerClasses"
            :style="{height: height + 'px'}"
            @scroll="handleScroll"
            @wheel="onWheel"
            @touchstart="onPointerDown"
            ref="scrollContainer"
        >
        </div>
```
### @scroll="handleScroll"

 使用函数节流降低滚动事件的触发频率
``` js
    this.handleScroll = throttle(this.onScroll, 150, {leading: false});
```
通过计算容器clientHeight， scrollTop， scrollHeight来计算是否达到下拉加载条件，设置变量是否需要触发触底事件，供 @wheel="onWheel"事件时使用。

### @wheel="onWheel"

在IVIEW的源码中发现，滚动事件并不能触发触底事件，只是做了设置了是否触底变量，只有在鼠标滚动的过程中才会根据是否触底来触发触底事件，这样做的好处是获取dom元素clientHeight， scrollTop， scrollHeight属性放到了节流的onScroll事件中，优化了性能。

## 查缺补漏
- Math.sign() 此函数共有5种返回值, 分别是 1, -1, 0, -0, NaN. 代表的各是正数, 负数, 正零, 负零, NaN。传入该函数的参数会被隐式转换成数字类型。