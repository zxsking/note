# mysql的基础操作

## 1.库操作

### 创建数据库

```mysql
CREATE DATABASE IF NOT EXISTS [数据库名] CHARACTER SET '[字符编码]';  #后可指定字符编码
例:CREATE DATABASE IF NOT EXISTS mybatis CHARACTER SET utf8;  
```

### 查看数据库

```mysql
show databases;
```

### 修改表名

```mysql
rename table [旧表名] to [新表名]
```

### 删除数据库

```mysql
DROP DATABASE IF EXISTS [数据库名];
```

### 使用数据库

```mysql
use [数据库名]
```

## 2.表操作

### **创建表**

```mysql
CREATE TABLE IF NOT EXISTS [表名] (
    [字段名] [字段类型],
    [字段名] [字段类型]，
    [字段名] [字段类型]，
    .....
);
```

### 查看表结构

```mysql
DESC [表名];  #可用来
```

### 查看表全部数据

```mysql
select *
from [表名];
```

### 删除表

```mysql
DROP TABLE IF EXISTS [表名];
```

### **添加字段**

```mysql
alter table [表名]  add [字段名] [字段类型];
```

### 删除字段

```mysql
alter table [表名] drop [字段名];
```

### 修改字段名及修改字段属性

```mysql
#方法一 CHANGE  : 即可以修改字段的名称 也可以修改字段的属性
ALTER TABLE [表名]
CHANGE [旧字段名] [新字段名] [可填原本字段属性 或 修改过后的字段属性]

#方法二 MODIFY  : 只能修改列的属性 
ALTER TABLE [表名]
MODIFY [字段名] [新属性]
```

## 3.数据操作

### 删除表数据

```mysql
DELETE FROM [表名] WHERE [满足条件的数据]
```

### 添加数据

```mysql
INSERT INTO [表名](字段名1,字段名2,...,字段名n)
     VALUES(值1,值2,...,值n);
```

### 添加数据

```mysql
update [表名] set [字段名] = [字段类容] where [匹配字段];
例:	
更改pet表内的数据 将name 为 Claws 的owner的名称改为kevin
update pet set owner = 'kevin' where name = 'Claws';
```



## 4.其他功能

### 查询字符集

```
SHOW VARIABLES LIKE 'character%';
```

