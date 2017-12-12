# 系统布局框架
  整个系统的布局文件system，包括路由文件system.js、模板文件system.hbs、控制器system.js。

## 路由文件system.js
  用于定义整体布局的一些锚点事件
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
  /**
   * 循环每个有权限的机构来对该机构下的菜单进行排序
   */
  _.forEach(roleOrgs, roleOrg => {
    let menuList = roleOrg.menuList;
    if (menuList instanceof Array) {
      roleOrg.menuList = this.sortByMenuOrder(menuList);
    }
  });
  ~~~

### sortByMenuOrder
  对每个机构的菜单进行排序<br>
  1. 参数：<br>
    * menuList 需要排序的菜单对象数组
  1. 返回：排完序的菜单对象数组
  ~~~js
  /**
   * 循环递归给没有菜单数组及其下级菜单数组进行排序
  */
  menuList = _.orderBy(menuList, 'menuOrder', 'asc');
    _.forEach(menuList, menu => {
      var nextMenuList = menu.menuList;
      if (nextMenuList !== undefined) {
        menu.menuList = this.sortByMenuOrder(nextMenuList);
      }
    });
  ~~~
  
### getCurrentOrg
  获取当前机构，通过递归的方式获取最高级别有菜单的机构为当前机构<br>
  参数：<br>
  1. 参数：<br>
    * orgs 同一父机构的有权限的机构
    * roleOrgs 有权限的机构数组
  1. 返回：当前机构 如果没有返回null