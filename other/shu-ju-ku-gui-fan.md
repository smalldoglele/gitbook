1.表前缀的含义
 + tmp_ 临时表
 + sys_ 系统相关 
 + qrtz_ 定时任务 quartz
 + cms_
 + cgen_
 
2.通用列含义
 + id 主键表名加上id唯一
 + created:创建记录的日期
 + createdby:创建记录人的ID
 + updated:更新记录日期
 + updatedby:最后一次更新记录人的ID
 + deleted:是否逻辑存在（就是用户视图看不见，但物理数据仍在，用来控制数据在用户视图上显示的字段）
 + role_id:用户该记录角色人的ID号，如果为0表示超级管理员
 + post_id:拥有该记录权限的人的ID号，如果为0，则是系统管理员专用ID.
 + org_id: 拥有该记录组织机构的ID号，如果为某机构的ID，则该机构所有用户都可以拥有该类数据的访问权限。这些通用列前缀是这套ERP数据权限管理的根本。绝大部分表都有这个设计。
  
3.通用表设计
+ 人员 user user_member user_store 
+ 机构 org org_supplier org_customer 