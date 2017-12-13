# 系统布局框架
整个系统的布局文件system，包括路由文件system.js、模板文件system.hbs、控制器system.js。

## 路由文件system.js
用于定义整体布局的一些钩子事件

### setupController
启动控制器时进入的方法<br>
参数：<br>
* controller 控制器的实例对象
~~~js
let dropDownOrgs = user.orgs;   //当前机构以下的所有下级机构

let roleOrgs = user.roleOrgs;   //当前登录人能够切换的机构
~~~
`roleOrgs`可以切换的机构对象数组，对象里没有menuList字段为不能切换的机构，只是用于显示切换机构树的结构。

### sortMenuList
对所有组织的菜单进行排序<br>
参数：<br>
* roleOrgs 可以切换机构的对象数组

~~~js
_.forEach(roleOrgs, roleOrg => {
  /*
  * 循环每个有权限的机构来对该机构下的菜单进行排序
  */
  let menuList = roleOrg.menuList;
  if (menuList instanceof Array) {
    roleOrg.menuList = this.sortByMenuOrder(menuList);
  }
});
~~~

### sortByMenuOrder
对每个机构的菜单进行排序<br>
参数：<br>
* menuList 需要排序的菜单对象数组

返回：排完序的菜单对象数组

~~~js
//循环递归给没有菜单数组及其下级菜单数组进行排序
menuList = _.orderBy(menuList, 'menuOrder', 'asc');
  _.forEach(menuList, menu => {
    var nextMenuList = menu.menuList;
    if (nextMenuList !== undefined) {
      menu.menuList = this.sortByMenuOrder(nextMenuList);
    }
  });
~~~
  
### getCurrentOrg
获取当前机构，通过递归的方式获取最高级别到最底级别有菜单的机构为当前机构<br>
参数：<br>
  * orgs 同一父机构的有权限的机构
  * roleOrgs 有权限的机构数组

返回：当前机构 如果没有返回null

## 控制器system.js
  用于定义一些同名模板里的事件和逻辑<br>

### pathChange
banner组件成功切换组织执行的方法，用于切换菜单、清除一些缓存数据<br>
参数：<br>
* org 当前需要切换的机构对象
* orgs 当前切换机构的树结构路径对象数组

### logoutSystem
banner组件点击退出上传事件执行的方法，用于执行退出登录接口，清除session里的缓存信息，退出到登录页面

### selectMainMenu
  一级菜单组件

### secMenuSidebarSelect

### selectSecMenu

### selectThirdMenu

### thirdMenuSidebarSelect

## 模板文件system.hbs
整理布局的模板文件，使用了以下组件：
* sys-banner  显示banner的组件
* main-menu  显示左侧一级菜单的组件
* second-menu  显示右侧顶部的二级菜单组件
* third-menu  显示右侧二级目录下的三级菜单组件
* warn-table  显示血糖报警列表组件
* form-handle-warn  工作台中关闭血糖报警时，出现的处理弹框