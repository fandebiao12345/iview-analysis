## Mixin
### emitter.js
#### dispatch
这个方法是触发自定义事件，通过传递componentName来触发想要触发的组件自定义事件。
- componentName(组件名)
- eventName(自定义事件名)
- params(参数)

首先获取当前组件的父组件，如果没有父组件就会获取自己，然后获取刚刚获取的组建名，如果组建名与传入的组建名一致，就会直接触发事件，如果不是，则会向上递归，这里iview巧妙的使用了while 来做向上递归,直到找到组建名一致或$parent为空。

``` js

    dispatch(componentName, eventName, params) {
            let parent = this.$parent || this.$root;
            let name = parent.$options.name;

            while (parent && (!name || name !== componentName)) {
                parent = parent.$parent;

                if (parent) {
                    name = parent.$options.name;
                }
            }
            if (parent) {
                parent.$emit.apply(parent, [eventName].concat(params));
            }
        },
```