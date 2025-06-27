大家好，欢迎回来鸿蒙5莓创图表组件的专场，很多小伙伴都不知道每个图表类型中的属性到底是干嘛的，怎么用。所以我们将详细去讲解每个属性，跟我一起学习吧。

我们这一期来讲解McLineChart折线图组件中title属性的详细用法。这个属性控制着图表的标题显示，包含主副标题的样式、位置、动画等丰富配置。下面我们将逐个属性进行深度解析，并提供完整代码示例。

### 1. show属性

作用：控制标题是否显示

类型：Boolean

默认值：true

可选值：true | false

场景：当需要动态切换标题显示状态时使用

title: { show: false // 隐藏标题 }

### 2. text属性

作用：设置主标题文本内容

类型：String

默认值：''（空字符串）

场景：展示图表的核心说明文字

title: { text: '2023年销售趋势' // 主标题内容 }

### 3. subtext属性

作用：设置副标题文本内容

类型：String

默认值：''（空字符串）

场景：补充说明或数据单位标注

`title: { subtext: '单位：万元' // 副标题内容 }`

### 4. direction属性

作用：控制主副标题排列方向

类型：String

默认值：'column'（垂直排列）

可选值：'column' | 'row'

场景：需要横向并排显示主副标题时

`title: { direction: 'row' // 水平排列 }`

### 5. itemGap属性

作用：设置主副标题间距

类型：Number

默认值：5

场景：调整标题之间的紧凑程度

`title: { itemGap: 10 // 增大间距 }`

### 6. 位置控制属性组

包含`left/right/top/bottom`四个子属性：

● 作用：控制标题容器的定位

● 类型：String | Number

● 默认值：'auto'

● 示例值：'10%' | 20（像素值）

● 场景：需要精确定位标题时使用

`title: { left: '20%', // 距离左侧20%宽度 top: 10 // 距离顶部10像素 }`

### 7. offset属性

作用：设置标题的像素偏移量 
类型：Array 默认值：[0, -20] 
格式：[水平偏移, 垂直偏移] 
场景：微调标题位置

`title: { offset: [10, 30] // 向右10px，向下30px }`

### 8. textStyle属性（对象）

控制主标题文本样式，包含以下子属性：

● color：文字颜色（String，默认'#333'）

● fontSize：字号（Number，默认36）

● fontWeight：字重（String，默认'bold'）

● fontFamily：字体（String，默认'sans-serif'）

● textAlign：水平对齐（String，默认'center'）

● textBaseline：垂直对齐（String，默认'bottom'）

`title: { textStyle: { color: '#1890FF', fontSize: 24, fontWeight: 'normal' } }`

### 9. subtextStyle属性（对象）

控制副标题文本样式，子属性同textStyle，区别在于：

● color默认'red'

● fontSize默认28

● fontWeight默认'400'

`title: { subtextStyle: { color: '#666', fontSize: 16 } }`

### 10. rLevel属性

作用：设置渲染层级

类型：Number

默认值：20

场景：需要控制标题与其他元素的遮盖关系时

`title: { rLevel: 100 // 提高渲染层级 }`

### 11. animationCurve属性

作用：设置标题显示动画曲线

类型：String

默认值：'easeOutCubic'

可选值：所有CSS动画曲线值

`title: { animationCurve: 'linear' // 线性动画 }`

### 12. animationFrame属性

作用：设置动画帧数

类型：Number

默认值：30

特殊值：0表示关闭动画

`title: { animationFrame: 50 // 更流畅的动画 }`

### 综合应用案例

每个属性的作用、类型、默认值、可选值、场景等都讲解完毕，接下来我们看看整体的综合示例


```
import { McLineChart, Options } from '@mcui/mccharts'

@Entry
@Component
struct Index {
  @State maxData: number[] = [11, 11, 15, 13, 12, 130, 10] // 初始化数据
  
  @State seriesOption: Options = new Options({
    title: {
      show: true,
      text: '气温数据',
      subtext: '2023年1-4月',
      direction: 'row',
      itemGap: 15,
      left: 'center',
      top: 20,
      textStyle: {
        color: '#1E88E5',
        fontSize: 28,
        fontFamily: 'Microsoft YaHei'
      },
      subtextStyle: {
        color: '#757575',
        fontSize: 16
      },
      animationCurve: 'easeInOutBack'
    },
    xAxis: {
      data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
    },
    series: [{
      name: '最高气温',
      data: this.maxData
    }]
  })

  // 动态修改数据
  aboutToAppear() {
    setTimeout(() => {
      // 传递需要修改的属性与数值，不需要全部传
    }, 2000)
  }

  build() {
    Row() {
      McLineChart({
        options: this.seriesOption
      })
    }
    .height('50%')
  }
}
```

### 实际场景拓展

在电商数据看板中，可以通过动态修改title.text实现：


```
// 根据筛选条件更新标题
function updateTitle(month: string) {
  // 更新数据源
  this.maxData = [110, 110, 150, 130, 120, 190, 100];
  this.minData = [-1, -2, -2, -5, 3, -2, 0];

  // 动态配置图表
  this.seriesOption.setVal({
    title: {
      text: `${month}月气温数据`,  // 主标题动态绑定月份
      subtext: `同比${data.growthRate}%`  // 副标题显示增长率
    },
    series: [
      { 
        name: '最高气温', 
        data: this.maxData  // 绑定最高温数据
      },
      { 
        name: '最低气温', 
        data: this.minData   // 绑定最低温数据
      }
    ]
  });
}
```

好，这期讲到这里就结束了，希望大家通过本文能全面掌握McLineChart标题组件的使用技巧，在实际开发中灵活运用这些属性打造专业级数据可视化效果。我们下期再见！