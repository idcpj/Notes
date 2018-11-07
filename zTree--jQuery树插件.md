
[TOC]

> [官网](http://www.treejs.cn/v3/demo.php#_304)


## 配置
```
    var setting = {
    view: {
        selectedMulti: true, //设置是否能够同时选中多个节点
        showIcon: true,      //设置是否显示节点图标
        showLine: true,      //设置是否显示节点与节点之间的连线
        showTitle: true,     //设置是否显示节点的title提示信息
    },
    data: {
        simpleData: {
            enable: ture,   //设置是否启用简单数据格式（zTree支持标准数据格式跟简单数据格式，上面例子中是标准数据格式）
            idKey: "id",     //设置启用简单数据格式时id对应的属性名称
            pidKey: "pId"    //设置启用简单数据格式时parentId对应的属性名称,ztree根据id及pid层级关系构建树结构
        }
    },
    check: {
        enable: true         //设置是否显示checkbox复选框
    },
    callback: {
        onClick: onClick,             //定义节点单击事件回调函数
        onRightClick: OnRightClick,   //定义节点右键单击事件回调函数
        beforeRename: beforeRename,   //定义节点重新编辑成功前回调函数，一般用于节点编辑时判断输入的节点名称是否合法
        onDblClick: onDblClick,       //定义节点双击事件回调函数
        onCheck: onCheck              //定义节点复选框选中或取消选中事件的回调函数
    },
    async: {
        enable: true,                      //设置启用异步加载
        type: "get",                       //异步加载类型:post和get
        contentType: "application/json",   //定义ajax提交参数的参数类型，一般为json格式
        url: "/Design/Get",                //定义数据请求路径
        autoParam: ["id=id", "name=name"]  //定义提交时参数的名称，=号前面标识节点属性，后面标识提交时json数据中参数的名称
        dataFilter: filterFuction
    }
};
```
## zTree的数据格式
```
treeNode: {
    name,       //节点显示的文本
    checked,    //节点是否勾选，ztree配置启用复选框时有效
    open,       //节点是否展开
    icon,       //节点的图标
    iconOpen,   //节点展开式的图标
    iconClose,  //节点折叠时的图标
    id,         //节点的标识属性，对应的是启用简单数据格式时idKey对应的属性名，并不一定是id,如果setting中定义的idKey:"zId",那么此处就是zId
    pId,        //节点parentId属性，命名规则同id
    children,   //得到该节点所有孩子节点，直接下级，若要得到所有下属层级节点，需要自己写递归得到
    isParent,   //判断该节点是否是父节点，一般应用中通常需要判断只有叶子节点才能进行相关操作，或者删除时判断下面是有子节点时经常用到。
    getPath()   //得到该节点的路径，即所有父节点，包括自己，此方法返回的是一个数组，通常用于创建类似面包屑导航的东西A-->B-->C 
}
```
## 提示
1.如果想显示内容为所有的文件夹,修改icon
```
for(var i=0;i<json.length;i++){
	json[i].icon = "/Public/Admin/img/folder.png";//修改所有图片为 文佳夹
	if (i == 0) 
		json[i].open = 1 ;  //默认打开第一层
}
``