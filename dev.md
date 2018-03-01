Vue.js use a fork of [snabbdom](https://github.com/snabbdom/snabbdom).

https://www.jianshu.com/p/d981a03f7029?from=timeline&isappinstalled=0

https://www.zhihu.com/question/46397274

https://github.com/answershuto/learnVue

https://github.com/violetjack/VueStudyDemos

Vue 2.0 为什么选用 Flow 进行静态代码检查而不是直接使用 TypeScript？

尤雨溪：这个选择最根本的还是在于工程上成本和收益的考量。Vue 2.0 本身在初期的快速迭代阶段是用 ES2015 写的，整个构建工具链也沿用了 Vue 1.x 的基于 ES 生态的一套（Babel, ESLint, Webpack, Rollup...)，全部换 TS 成本过高，短期内并不现实。相比之下 Flow 对于已有的 ES2015 代码的迁入/迁出成本都非常低：
1. 可以一个文件一个文件地迁移，不需要一竿子全弄了。
2. Babel 和 ESLint 都有对应的 Flow 插件以支持语法，可以完全沿用现有的构建配置；
3. 更贴近 ES 规范。除了 Flow 的类型声明之外，其他都是标准的 ES。万一哪天不想用 Flow 了，用 babel-plugin-transform-flow-strip-types 转一下，就得到符合规范的 ES。
4. 在需要的地方保留 ES 的灵活性，并且对于生成的代码尺寸有更好的控制力 (rollup / 自定义 babel 插件）
 
第三点额外说一些：这一点上 Facebook 应该也是同样的考量，宁可贴近规范而不是用一个被 M$ 控制的、一旦使用难以迁出的语言。为什么 Angular 就愿意用 TS 呢？因为 Angular 本来就是一帮搞 Java 的人弄出来的，而且只是 Google 的一个子项目，Google 在公司层面根本不关心它用什么语言。而对 Facebook 来说 React/ReactNative/Babel/Flow/Nuclide 是整个公司 infrastructure 层面的东西，要么依赖规范，要么就得自己有控制权。

编辑器 / IDE 方面，Atom + Nuclide 其实也还凑合，type warning / type hint / autocomplete / jump to definition 都有，就是 Atom 本身慢了点。至于重构、设计什么的，我只想说，看的是使用的人的水平，跟用什么语言没那么大关系。水平烂的人用 TS 一样写的是翔一样的代码，看看 java 就知道了。另外注意我并没有说 TS 不好，但是在 Vue 的需求和现状下 Flow 是更合理的选择。