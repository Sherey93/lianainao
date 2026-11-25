# lianainao · 妈妈的恋爱脑拯救计划

角色卡「妈妈的恋爱脑拯救计划」的状态栏前端页面（本卡专用版：通用面板 V2 + 头像）。

## 卡里怎么加载

| 用途 | 文件 | 地址 |
|---|---|---|
| 面板本体 | 仓库根 index.html | https://testingcf.jsdelivr.net/gh/Sherey93/lianainao@<commit>/index.html |
| 头像 | 仓库根 vatar.webp | https://testingcf.jsdelivr.net/gh/Sherey93/lianainao@<commit>/avatar.webp |

两处都**钉死 commit 号**，不写 @main：jsDelivr 对分支引用缓存约 12 小时，purge 工具对 testingcf 镜像实测无效（报 finished 但仍给旧字节）；commit 号是不可变路径，任何镜像都立刻给最新文件。

## 这文件是怎么来的

1. 源码：	avern_helper_template 的 src/妈妈的恋爱脑拯救计划/界面/状态栏/
   （从 src/通用面板V2/界面/状态栏/ 复制而来，改了三处：姓名左侧加圆形头像、schema.ts 换成这张卡的变量结构、补 字段结构 导出）
2. 构建：模板仓库里 
ode node_modules/webpack-cli/bin/cli.js --config webpack.card.mjs --mode production
   （webpack.card.mjs 只构建本卡这一条，并摘掉官方配置里会 spawn pnpm 的两个插件）
3. 产物：dist/妈妈的恋爱脑拯救计划/界面/状态栏/index.html
4. 发布前把 <script type="module"> 替换成 <script>：bundle 里没有 import/export，改当经典脚本后由 jQuery 的 $('body').load() 直接执行，不走模块脚本那条路
5. 上传为仓库根 index.html

## 头像

- 来源：D:\ACARD\图库\2.png，按「腰以上」裁成正方形，缩到 384×384，存成 WebP（17 KB）
- 面板里靠 order-radius: 50% + object-fit: cover 裁成圆形，不改图片本身
- 换头像：重新裁图覆盖 vatar.webp 并 push，再把新 commit 号写回面板源码 App.vue 的 头像地址，重新构建发布

## 说明

- 面板靠酒馆助手注入的 MVU 变量渲染，**只读不写**，不会动 世界（阶段、炮灰、被撞见风险）
- 断网或 jsDelivr 不通时状态栏显示不出来，正文不受影响
- 改了文件后 jsDelivr 有缓存，改完记得把新 commit 号写进卡里的正则再重新打包