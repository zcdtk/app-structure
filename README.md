# 应用程序结构模型

在常规的应用程序（以下简称 app）由多个部分组成，将一个 app 根据不同的功能做结构化拆解，发现应用的主要组成有应用组织、视图、数据服务和元数据等几个部分组成。

结构化应用程序的意义，在于开发人员对应用的构成，有一个清晰明了的定义，明确基于程序文件的那一部分，定了什么样的功能，在应用程序中，处于何种定位，方便开发人员理解和参与内容优化。

应用程序，结构如下：

![应用程序结构](imgs/app-structure.png)

## 应用组织

应用组织，在 app 中，为其提供应用级功能性内容，成员如下：

- 主题：提供应用级样式，应用程序可以切换不同样式，通过主题切换，为界面提供不同的样式展现。
- 多语言：多语言是前端必备的功能点，面向多样化的用户场景。
- 资源：app 内图片、图标等资源文件。
- 功能组件：登录页面、注销页面、404 页面、 500 页面等功能组件，该组件一般不会复用。

应用组织的内容，多为 app 所必须的结构，补充 app 所能提供的功能。



埃毕致前端模型，在适配应用组织成员上，做了比较多的结构设计，可以为 app 构建对于的应用组织成员。

组织模型化支持如下表：

| 应用组织 | 模型名称     | 详情                                                         | 备注    |
| -------- | ------------ | ------------------------------------------------------------ | ------- |
| 主题     | 应用界面主题 | [IPSAppUITheme](https://modelapi.ibizlab.cn/#/net/ibizsys/model/app/theme/IPSAppUITheme) |         |
| 多语言   | 应用多语言   | [IPSAppLan](https://modelapi.ibizlab.cn/#/net/ibizsys/model/app/IPSAppLan) |         |
| 资源     | 系统图片资源 | [IPSSysImage](https://modelapi.ibizlab.cn/#/net/ibizsys/model/res/IPSSysImage) |         |
| 功能组件 | 应用功能页面 | [ IPSAppUtilPage](https://modelapi.ibizlab.cn/#/net/ibizsys/model/app/IPSAppUtilPage) |         |
| . . .    | .  .  .      | .  .  .                                                      | .  .  . |

应用界面主题模型，应该包含一整套的模型内容，主题所需的必备点在模型中，应该做关系约束比较好，有需要可以做模型补充，约束结构如下所示：

![theme](imgs/theme.png)



## 视图

视图时 app 的内容单位，视图本身属于组件的一种。

视图组为独立的功能结构来做说明，是因为视图本都属于 app 业务结构的抽象集合。一个视图，就是一个完整业务能力在 app 中的表现，app 通过不同的视图，展示不同业务需要，构建可以重复使用的内容单位。

文本将功能组件与视图做出区别，就在于组件是否被基于业务重复使用。功能组件一般只有特定条件才会被 app 访问，视图则会在整个 app 会被重复使用。

视图成员如下：

- 逻辑：视图拥有的数据处理代码结构。

- 视图模型：视图数据模型。
- 提示消息：视图提示消息，一般放置静态的 Alert 类提示信息。
- 布局：视图内容布局，将组件在不同的位置展示。
- 组件：视图业务数据的抽象单位。
  - 组件成员：部分组件会实现更加细化的抽象结构，如表单中的数据编辑对象。
  - 提示消息：组件提示消息，一般分为静态和动态。静态消息和视图消息类似，动态消息主要为组件数据加载、处理后的提示信息。
  - 逻辑：部分组件除了数据加载逻辑之外，会附加其他处理，如删除、编辑等，常见于表格或者列表中。



埃毕致前端模型，针对视图提供了 [应用视图模型（IPSAppView）]( https://modelapi.ibizlab.cn/#/net/ibizsys/model/app/view/IPSAppView ) ，该视图模型为常规视图提供所需的视图布局、逻辑等一系列内容，以下几个结构以 应用视图模型适配视图成员做出说明。



### 逻辑

> 注：本章节中提到的部件，将在组件章节做出介绍。

逻辑作为交互功能的代码单位，在视图中有非常重要的地位。它是视图业务的表现，也是数据处理的重要环节。

埃毕致前端模型中，逻辑模型本身是中立的，它并不针对场景设计逻辑模型。一般是定义好模型之后，将模型挂载到视图上，模型落地即成为视图模型；将模型挂载到部件上，模型落地即成为部件模型。

除了基于视图交互所定义的模型之外，埃毕致前端模型还预置引擎逻辑，数据校验等其他的逻辑模型。

埃毕致前端现有的模型能力，基本能适配常见的视图逻辑内容，详情如下：

| 模型名称             | 详情                                                         | 备注    |
| -------------------- | ------------------------------------------------------------ | ------- |
| 界面行为             | [ IPSUIAction](https://modelapi.ibizlab.cn/#/net/ibizsys/model/view/IPSUIAction) |         |
| 应用视图逻辑         | [IPSAppViewLogic](https://modelapi.ibizlab.cn/#/net/ibizsys/model/app/view/IPSAppViewLogic) |         |
| 应用视图逻辑引用视图 | [ IPSAppViewLogicRefView](https://modelapi.ibizlab.cn/#/net/ibizsys/model/app/view/logic/IPSAppViewLogicRefView) |         |
| 应用视图新建数据逻辑 | [ IPSAppViewNewDataLogic](https://modelapi.ibizlab.cn/#/net/ibizsys/model/app/view/logic/IPSAppViewNewDataLogic) |         |
| 实体打开数据视图逻辑 | [ IPSAppViewOpenDataLogic](https://modelapi.ibizlab.cn/#/net/ibizsys/model/app/view/logic/IPSAppViewOpenDataLogic) |         |
| 应用部件逻辑         | [ IPSControlLogic](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/IPSControlLogic) |         |
| 系统内置视图引擎     | [IPSViewEngine](https://modelapi.ibizlab.cn/#/net/ibizsys/model/view/IPSViewEngine) |         |
| .  .  .              | .  .  .                                                      | .  .  . |

埃毕致逻辑模型在 app 上的交互结构，可以从下图说明：

![逻辑交互](imgs/logicaction.png)

逻辑在视图和部件内部，本身具有完整的处理逻辑，作为载体，逻辑在其内部是封闭的。

同时，视图和部件，也可以通过逻辑进行交互，它是二者数据流向的的通道。



### 视图模型

视图模型是由前端开发人员组织生成和维护的视图数据层。 

在应用视图模型中，并没有提供相应的视图模型对象，给需要使用的 app 程序直接消费。但是，应用视图模型本身具备有视图模型所需变量，模型使用人员可以通过应用视图模型构建前端所需的



### 视图结构

视图是 app 的主要表现内容，在应用程序中，内容的构成与业务的呈现，都由视图承载。

- 视图模型：视图数据模型和展现逻辑
- 视图消息：视图内容补充
- 布局：视图内容结构化处理
- 逻辑：系统逻辑在视图上的承载点
- 部件：业务数据的不同抽象结构
  - 部件成员：构建部件的内容
  - 部件消息：部件静态消息和动态消息
  - 逻辑：部件作为逻辑的承载点

视图模型结构如下表：

| 构成     | 模型名称     | 详情                                                         |
| -------- | ------------ | ------------------------------------------------------------ |
| 视图消息 | 视图消息     | [ IPSViewMsg](https://modelapi.ibizlab.cn/#/net/ibizsys/model/view/IPSViewMsg) |
| 布局     | 视图布局面板 | [ IPSViewLayoutPanel](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/panel/IPSViewLayoutPanel) |



### 部件

在视图中，部件是视图内容数据表现最丰富的部分。数据的表现形式的不同，将其抽象成不同的业务对象，常见的有表单、表格、树、图表和日历等。

常见的部件及模型如下：

| 部件   | 模型名称       | 详情                                                         |
| ------ | -------------- | ------------------------------------------------------------ |
| 表格   | 实体表格       | [ IPSDEGrid](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/grid/IPSDEGrid) |
| 表单   | 实体表单       | [ IPSDEForm](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/form/IPSDEForm) |
| 树     | 实体树视图部件 | [ IPSDETree](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/tree/IPSDETree) |
| 菜单   | 应用菜单       | [ IPSAppMenu](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/menu/IPSAppMenu) |
| 图表   | 实体图表控件   | [ IPSDEChart](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/chart/IPSDEChart) |
| 日历   | 日历部件       | [ IPSCalendar](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/calendar/IPSCalendar) |
| 向导   | 实体向导面板   | [IPSDEWizardPanel](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/wizardpanel/IPSDEWizardPanel) |
| 列表   | 实体列表控件   | [IPSDEList](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/list/IPSDEList) |
| 、、、 | 、、、         | 、、、                                                       |

部件的组成，主要包括部件成员、部件消息和逻辑等。逻辑的结构，和视图基本一致，此处不做介绍。

#### 部件消息

部件消息一般分为静态消息和动态消息两个部分，静态消息固定在部件的内容中，部件渲染，直接出现。动态消息一般在部件做逻辑交互时，做提示使用，丰富部件的业务逻辑交互效果。同时，部件消息提供多语言支持。

部件消息模型如下：

| 模型名称 | 详情                                                         |
| -------- | ------------------------------------------------------------ |
| 部件消息 | [ IPSCtrlMsg](https://modelapi.ibizlab.cn/#/net/ibizsys/model/res/IPSCtrlMsg) |

#### 部件成员

部件成员，是部件的组成部分，其中最具代表性的是表单部件及其成员。

表单部件基于不同的功能，将其成员分为以下几个：

| 名称名称             | 详情                                                         |
| -------------------- | ------------------------------------------------------------ |
| 表单按钮部件         | [ IPSDEFormButton](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/form/IPSDEFormButton) |
| 表单关系界面部件     | [ IPSDEFormDRUIPart](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/form/IPSDEFormDRUIPart) |
| 表单IFrame部件       | [ IPSDEFormIFrame](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/form/IPSDEFormIFrame) |
| 实体表单分页部件分页 | [IPSDEFormTabPage](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/form/IPSDEFormTabPage) |
| 实体表单分页         | [ IPSDEFormPage](https://modelapi.ibizlab.cn/#/net/ibizsys/model/control/form/IPSDEFormPage) |
| 、、、               | 、、、                                                       |

作为表单的成员，他们共同构成了表单界面常规表现所需的模型结构，并在其中承担不同的更深层次的子内容展示。

## 数据服务

数据服务，属于应用中业务能力抽象处理的中间层。常见的由公共 API 管理对象，提供部分逻辑处理，为界面提供数据。

提供数据服务方式及特点如下：

- 远程：通过 http 请求获取数据，具有前台与后台的交互过程，在处理请求时，同时提供其他功能。
  - 权限：请求过程动态授权。
  - API：公共的 API 管理。
  - 数据格式化：将获取的数据格式化处。
  - 多维数据约束：使用数据关系能力约束。
- 本地：在浏览器中获取数据。
  - 缓存：从浏览器中获取数据，解析获取所需部分。
  - 数据库：从浏览器数据库中读取数据。

数据服务在现有的技术框架中，Angular 的服务对象，基本能合适的匹配数据服务功能。该框架中的服务对象，对每个组件提供服务能力，其中有数据获取、API 维护和数据格式化等常见功能。

本文示例如下：

![数据服务](imgs/data-service.png)

在上述代码示例中，基于数据关系的能力，在 URL 中通过层级访问路径得以体现。数据对象的主键作为约束能力的部分内容，成为了权限和多维数据约束在实际应用中的具体场景。

## 元数据

 元数据是关于数据的组织、数据域及其关系的信息，简言之，元数据就是关于数据的数据。

其成员如下：

- 元素：数据成员，构成元数据的基本组成的单位。
- 元素值规则：元素基本类别，如文本、时间、数值等，另外提供复杂值规则，如正则、值范围等等。
- 数据模型：提供的数据结构。
- 数据关系：对象之间的主从关系，表现为数据之间的约束。
- Mock 数据：模拟真实业务数据。

元数据在应用程序中，是基于业务表现的一种数据处理结果。