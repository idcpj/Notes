[TOC]

> [参考网址](https://blog.csdn.net/sinat_36329815/article/details/73549702)



2. 带引入参数的形式
```
function getTreeFromArray($arr , $pid = 0,&$tree){
    foreach ($arr as $k => $v){
        //遍历数组，如果当前元素父id与本层级的父id相等则加入$tree
        if($v['dept_parent_id'] == $pid){
            $tree[$k] =  $arr[$k];
            //加入后删除该元素减少后序遍历次数，提升性能
            unset($arr[$k]);
            //使用递归方式查找该元素的子节点数组
            $tree[$k]['sub_department'] = $this->getTreeFromArray($arr,$v['department_id'],$tree);
        }
    }
}
```