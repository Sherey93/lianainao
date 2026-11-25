# lianainao · 妈妈的恋爱脑拯救计划

角色卡「妈妈的恋爱脑拯救计划」的状态栏前端页面（通用面板 V2 的运行版本）。

## 卡里怎么加载

仓库根目录 index.html，卡内正则「状态栏界面」加载地址：

https://testingcf.jsdelivr.net/gh/Sherey93/lianainao@main/index.html

## 这文件是怎么来的

1. 源码在 	avern_helper_template 的 src/通用面板V2/界面/状态栏/
2. 在模板仓库里 pnpm build，产物：dist/通用面板V2/界面/状态栏/index.html
3. 产物里 webpack 写的是 <script type="module">；本项目发布时把这一处替换成 <script>
   —— bundle 里没有任何 import/export，改当经典脚本后由 jQuery 的 $('body').load() 直接执行，
   少一条模块脚本的路径依赖。重新构建后记得重复这一步再上传。
4. 上传为本仓库根目录 index.html

## 说明

- 面板靠酒馆助手注入的 MVU 变量渲染，只读不写，不会改动变量
- 断网或 jsDelivr 不通时状态栏显示不出来，正文不受影响
- 改了 index.html 后 jsDelivr 有缓存，需要到 https://www.jsdelivr.com/tools/purge 刷新，
  或等约 12 小时自动更新