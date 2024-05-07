# 常用属性

>![[Pasted image 20240116211235.png]]

```javascript
var option1 = {
    // 设置颜色为天蓝色和浅灰色
    color: ['skyblue', '#d3d3d3'],
    // 设置提示框的触发类型为数据项图形触发
    tooltip: {
        trigger: 'item'
    },
    // 设置图例组件的位置在顶部居中
    legend: {
        top: '5%',
        left: 'center'
    },
    // 设置系列列表
    series: [
        {
            // 设置系列名称为'mk'
            name: 'mk',
            // 设置图表类型为饼图
            type: 'pie',
            // 设置饼图的半径范围
            radius: ['70%', '85%'],
            // 避免标签重叠
            avoidLabelOverlap: false,
            // 设置标签样式
            label: {
                show: false,
                position: 'center'
            },
            // 设置饼图强调样式
            emphasis: {
                label: {
                    show: true,
                    fontSize: 40,
                    fontWeight: 'bold'
                }
            },
            // 设置标签线样式
            labelLine: {
                show: false
            },
            // 设置饼图数据
            data: [
                // 设置数值为变量mk的值
                { value: mk },
                // 设置数值为800减去变量mk的值
                { value: 800 - mk }
            ],
            // 设置标签样式
            label: {
                show: true,
                position: 'center',
                // 设置标签内容格式
                formatter: '{a|MaxKill}\n{b|' + mk + '}' ,
                // 设置富文本样式
                rich: {
                    a: {
                        color: 'skyblue',
                        fontSize: 10,
                        lineHeight: 30
                    },
                    b: {
                        color: '#d3d3d3',
                        fontSize: 20,
                        lineHeight: 40
                    }
                }
            }
        }
    ]
};
```



1. **color**: 用于设置图表的颜色，可以是单个颜色值，也可以是颜色数组，用于设置不同系列或数据的颜色。
2. **tooltip**: 用于配置提示框组件的相关属性，包括触发类型（trigger）、提示框浮层的内容格式等。
3. **legend**: 用于配置图例组件的相关属性，包括位置（top、left等）和图例项的内容。
4. **series**: 用于配置系列列表。在你的代码中，每个图表都包含了一个series属性，用于配置环形图的具体数据和样式。
5. **radius**: 用于设置环形图的半径，可以通过设置内半径和外半径来调整环形图的大小。
6. **label**: 用于配置标签的样式和内容，包括是否显示、位置、格式化等。
7. **emphasis**: 用于配置图形的高亮样式，当鼠标悬停在图形上时会显示的样式。
8. **labelLine**: 用于配置标签的视觉引导线样式。