##关于使用 react-fast-unmount  npm包,下面是他的详细使用方法和介绍 
    
###说在前面，为什么需要这个包呢？
####使用react组件时候在数据加载还没完成 或者执行一些类似onscroll方法 ，组件销毁时后还改变数据报错如下：
   > Can't perform a React state update on an unmounted component. 
   > This is a no-op, but it indicates a memory leak in your application. 
   > To fix, cancel all subscriptions and asynchronous tasks in the componentWillUnmount method.

###直接引用
```jsx
import unject_unmount  from 'react-fast-unmount'
```
    然后再 自己需要的类上 @unject_unmount
```jsx
@unject_unmount
class Home extends PureComponent {
    ....
}
```
####当然 当你使用Decorator 修饰符的 你可能会遇到这样的报错

    > SyntaxError: C:UsersAdministratorDesktoptetestsrcapp.js: Support for the experimental syntax 'decorators-legacy' isn't currently enabled (15:1):

#####第一个解决方法：删除package.json中的babel配置，然后在.babelrc文件中的presets加上"react-app"
```jsx
####当然 当你使用Decorator 修饰符的 你可能会遇到这样的报错

    > SyntaxError: C:UsersAdministratorDesktoptetestsrcapp.js: Support for the experimental syntax 'decorators-legacy' isn't currently enabled..

#####第一个解决方法：删除package.json中的babel配置，然后在.babelrc文件中的presets加上"react-app"

```jsx
{
  "presets": ["@babel/preset-env", "react-app"],
  "plugins": [
    ["@babel/plugin-proposal-decorators", { "legacy": true }],
    ["@babel/plugin-proposal-class-properties", { "loose": true }]
  ]
}
```
#####第二个解决方法：使用react-app-rewired，来扩充create-react-app配置（比上面的方法更好，使用方法参考
```jsx
//配置文件   config-overrides.js

const { injectBabelPlugin } = require('react-app-rewired');
module.exports = function override(config, env) {
    // do stuff with the webpack config...
    config = injectBabelPlugin(['@babel/plugin-proposal-decorators', { "legacy": true }], config)   //{ "legacy": true }一定不能掉，否则报错
    return config;
};
```
[Learn how to use Decorator in your own project ,please refer to..](https://reactjs.org/docs/getting-started.html).






