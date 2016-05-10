# 运营统计

## Last modify date
	robin gao 2016-05-05

## Class 
	/vsa_web/src/main/leader/et/vis/leader/api/HomeAPI.java

## Path
	http://localhost:80/vsaapi/leader/homepage

## Http type
	GET

## Param
 	@param user_id 用户id
 	@param corp_id 公司id

## Authentication
	需要验证身份
	
## Return
	{"code":"200",
	日开单量,周开单量,月开单量,本月任务完成率,本周任务完成率
	"message":["true","0","1,020.0100","1,160.8916","22.52","17.11"],
	近7天开单量
	"dayvo":["true",[["2016-04-27","1020.00"],["2016-04-26","0.01"]]],
	近3个月 销量和任务量对比
	"monthvo":["true",[["2016-02","666.67","94.86"],
	["2016-03","666.67","1124.11"],["2016-04","666.67","150.11"]]]}

## Exception
   {"code":"200","message":"请绑定营销组织"}


