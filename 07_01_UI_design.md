# **UI设计** 

### 总览

按照项目前期调研和项目愿景，注重系统的简洁性和实用性。客户端：通过扫码直接进入点餐页面，不设置登录操作。整个点餐系统逻辑上分成四个页面：商家详情页面、菜单选购页面、订单页面和支付页面。
商家端：可以自由地管理客户端的菜品，实现菜品的增加删除修改，管理订单。

## 客户端

### 菜单选购界面
总体上按照现有常见的点餐小程序设计思路，左一栏是对菜品的分类，右边用列表的形式对单个菜品进行展现。
视觉效果上，考虑到交互性，菜品分类栏采用了扁平化设计，可以更加简单直接的将信息和事物的工作方式展示出来，减少认知障碍的产生；同时扁平化设计的视觉效果更简约，条理清晰，最重要的一点是，有更好的适应性。
为了使画面不显得拥挤，右边栏的菜品列表栏采用了卡片设计，这里扁平设计已经不适合多维度信息的表达。
![UI_choose](img/UI_diagram/Mainpage.PNG)
### 订单页面
![UI_choose](img/UI_diagram/OrderPage.png)
### 支付界面
点击订单页面下方“提交订单”直接跳转到支付页面。支付页面显示了四种支付方式及需要支付的金额，主要是为了使用户加强确认要支付的金额，避免出现金钱交易错误。若想取消订单，直接点击页面左上方"返回"键，可取消支付。
![UI_choose](img/UI_diagram/PayPage.PNG)
![UI_choose](img/UI_diagram/CancelPay.PNG)
### 商家详情页面
![UI_choose](img/UI_diagram/InfoPage.PNG)

## 商家端

### 登录页面
![UI_choose](img/UI_diagram/Login.png)
### 信息页面
![UI_choose](img/UI_diagram/InfoManage.PNG)
### 菜单页面
![UI_choose](img/UI_diagram/DishManage.png)
### 订单页面
![UI_choose](img/UI_diagram/OrderManage.png)

### 自评

- 设计逻辑清晰，视觉效果简约；
- 界面设计注重用户体验，操作方便；
- 设计的创新性有待提高