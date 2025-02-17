## Resolve_ORA-02292(外键)
    ```
    --查询表1有哪些约束
    select * from 表1 u where u.constraint_name like '%TB_ROLE%';
    --失效约束
    alter table 表1 disable constraint FK_TP_MENU_REFERENCE_TP_MENU cascade;
    alter table 表2 disable constraint FK_TB_ROLE__REFERENCE_TP_MENU cascade;
    --删除数据
    delete from 表1 t where t.status = 0;
    --生效约束
    alter table 表1 enable constraint FK_TP_MENU_REFERENCE_TP_MENU;
    alter table 表2 enable constraint FK_TB_ROLE__REFERENCE_TP_MENU;
    --查看数据
    select * from 表1;
    ```
