# dag_view


#### 基于该项目改造：https://github.com/xuhuihui/smallDemo/

#### 项目介绍
dag流程图

  改造点：
  
    （1）首次绘制svg时，把选中节点居中于可见区域，将g-root移动
    
    （2）选中节点时，突出当前节点以及上下游路径
    
    （3）基于bootstrap的右键菜单
    
    （4）样式调整

![界面示例](https://raw.githubusercontent.com/wiki/zhanghuang03/dag_view/images/pic.jpg "界面示例")


#### 

![界面示例](https://raw.githubusercontent.com/wiki/zhanghuang03/dag_view/images/core.png "界面示例")

[js/diag.js]把选中节点居中于可见区域 ，核心代码



```

        //缩放倍数
        var scale = 1.2;
        //转成translate坐标系
        svg.call(zoom.transform, d3.zoomIdentity.translate(0, 0).scale(scale));

        //可见坐标轴长度
        var axisVisLenX = svg._groups[0][0].clientWidth;
        var axisVisLenY = svg._groups[0][0].clientHeight;

        // g-root偏移原点坐标
        var gRootX = (svg._groups[0][0]).getElementsByTagName("g")[0].transform.baseVal[0].matrix.e;
        var gRootY = (svg._groups[0][0]).getElementsByTagName("g")[0].transform.baseVal[0].matrix.f;



        // 选中节点偏移g-root坐标
        var statePointX = (svg._groups[0][0]).getElementById(this.statePoint).transform.baseVal[0].matrix.e;
        var statePointY = (svg._groups[0][0]).getElementById(this.statePoint).transform.baseVal[0].matrix.f;


        // 选中节点偏移原点坐标 = g-root偏移原点坐标 + 选中节点偏移g-root坐标
        var totalTlX = statePointX + gRootX;
        var totalTly = statePointY + gRootY;

         

        // 把选中节点居中于可见区域，将g-root移动
        var nodeX = (totalTlX * scale - axisVisLenX / 2) * -1 ;
        var nodeY = (totalTly * scale - axisVisLenY / 2) * -1 ;
        svg.call(zoom.transform, d3.zoomIdentity.translate(nodeX, nodeY).scale(scale));
```

original project github link: https://d3js.org/
