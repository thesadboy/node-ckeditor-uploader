# school #############################################################

## 范式化

* admin 管理员用户名、密码 (2个)

	[用户名adminname]  [密码password]  [会话uSID]

* classes 班级(班长)
	
	[班级_id(追踪，重要)]  [班级名classname]  [密码password]  [会话uSID]

* students 学生

	[学生_id(追踪，重要)]  [学生帐号account_name]  [学生名name]  [班级_id(追踪，重要)]

* fees 账单

	[账单_id(追踪，重要)]  [账单金额money]  [最新日期join_date]  [提交标记commit(重要)]
	[学生_id(追踪，重要)]

* type 学生账户类型

	[学生_id(追踪，重要)]  [新用户标记is_new_account]

## 反范式化

* admin 管理员用户名、密码 (2个)

	[用户名adminname]  [密码password]  [会话usid]  [加入日期join_date]

{
    adminname : String,		管理员名
	password  : String,		密码
	usid      : String,		会话
	join_date : Date		加入日期
}

* classes 班级(班长)
	
	[班级_id(追踪，重要)]  [班级名classname]  [密码password]  [会话usid]  [加入日期join_date]

{
	_id : ObjectID,			班级_id(追踪，重要，不可改变)
	classname : String,		班级名
	password  : String,		密码
	usid      : String,	    会话
	join_date : Date		加入日期
}

* accounts 账单

	[学生_id]  [学生帐号account_name]   [学号stuid]  [学生名name]  [新用户标记is_new_account]
	[账单金额amount]  [最新日期join_date]  [提交标记is_commit(重要)]	
	[班级_id]

{
	_id 		   : ObjectID,	学生_id(追踪，重要，不可改变)
	class_id       : ObjectID,  班级_id
	account_name   : String,	学生帐号(唯一)
	name           : String,	学生名
    is_new_account : Boolean,	新用户标记
	amount         : Deceme,	账单金额
	join_date      : Date,		最新日期
	is_commit      : Boolean	提交标记
}

#####################################################################


___ ___ ___ 提交
___ ___ ___ 提交
...


标记“已提交”的账户不能修改

###################################################################### 

提取数据 -> “已提交0” "已提交1" “本班成员”

班长填写，提交 -> “已提交0”的数据被更新

管理员提交 -> “已提交0”的数据被提交，更新“已提交1”

## classes ###########################################################

* classes-entry 
* classes-login 
* classes-logout
	
	<form>[管理员名]  [密码]  [管理员名msg]  [密码msg]</form> 1

	__用户__  __密码__ >>

* classes-index
* classes-destroy

	<table>...
	      <tr><td>[班级_id]</td><td>[班级名]</td><td>[密码]</td><td>[...]</td><td>[加入时间]</td></tr> ...
	</table> 1

	__班级id__  __班级名__  __密码__  __...__  __加入时间__
	__班级id__  __班级名__  __密码__  __...__  __加入时间__
	__班级id__  __班级名__  __密码__  __...__  __加入时间__
	...

* classes-new 
* classes-create

	<form>[班级名]  [密码]  [...]  [班级名msg]  [密码msg]  [...msg]</form> ...

	__班级名__  __密码__  __...__  >>
	__班级名__  __密码__  __...__  >>
	__班级名__  __密码__  __...__  >>
	+

* classes-edit
* classes-update

	<form[班级_id]>[班级名]  [密码]  [...]  [班级名msg]  [密码msg]  [...msg]</form> ...

	__班级id__  __班级名__  __密码__  __...__  >>
	__班级id__  __班级名__  __密码__  __...__  >>
	__班级id__  __班级名__  __密码__  __...__  >>
	...

## accounts ###############################################################

* accounts-entry
* accounts-login 
* accounts-logout

	<form>[班级名]  [密码]  [班级名msg]  [密码msg]</form> 1

	__班级名__  __密码__ >>

* accounts-index
* accounts-destroy

	<table>...
	      <tr><td>[学生_id]</td><td>[学生账号]</td><td>[学号]</td><td>[学生名]</td><td>[...]</td><td>[加入时间]</td></tr> ...
	</table> 1

	__学生id__  __学生账号__  __学号__  __学生名__  __缴费金额__  __...__  __加入时间__
	__学生id__  __学生账号__  __学号__  __学生名__  __缴费金额__  __...__  __加入时间__
	__学生id__  __学生账号__  __学号__  __学生名__  __缴费金额__  __...__  __加入时间__
	...

* accounts-new 
* accounts-create

	<form>[学生账号]  [学号]  [学生名]  [...]  [学生帐号msg]  [学号msg]  [学生名msg]  [...msg]</form> ...

	__学生账号__  __学号__  __学生名__  __缴费金额__  __...__  >>
	__学生账号__  __学号__  __学生名__  __缴费金额__  __...__  >>
	__学生账号__  __学号__  __学生名__  __缴费金额__  __...__  >>
	+

* accounts-edit
* accounts-update

	<form[学生_id]>[学生账号]  [学号]  [学生名]  [...]  [学生帐号msg]  [学号msg]  [学生名msg]  [...msg]</form> ...

	__学生id__  __学生账号__  __学号__  __学生名__  __缴费金额__  __...__  >>
	__学生id__  __学生账号__  __学号__  __学生名__  __缴费金额__  __...__  >>
	__学生id__  __学生账号__  __学号__  __学生名__  __缴费金额__  __...__  >>
	...

# 完成 ################################################################

* admin-new       ok.
* admin-create    ok.
* admin-index     ...
* admin-edit      ...
* admin-update    ...
* admin-destroy   ...

* classes-entry   ok.
* classes-login   ok.
* classes-logout  ok.
* classes-new     ok.
* classes-create  ok.
* classes-index   ok.
* classes-edit    ok.
* classes-update  ok.
* classes-destroy ok.

* accounts-entry  ok.
* accounts-login  ok.
* accounts-logout ok.
* accounts-new    ok.
* accounts-create ok.
* accounts-index  ok.
* accounts-edit   ok.
* accounts-update ok.
* accounts-destroyok.

