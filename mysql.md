
# 1、什么是数据库？什么是数据库管理系统？什么是SQL？他们之间的关系是什么？
### 数据库：  
    
    英文单词DataBase，简称DB。按照一定格式存储数据的一些文件的组合。顾名思义：存储数据的仓库，实际上就是一堆文件。这些文件中存储了具有特定格式的数据。
  

### 数据库管理系统：
	
    DataBaseManagement，简称DBMS。
	数据库管理系统是专门用来管理数据库中数据的，数据库管理系统可以
	对数据库当中的数据进行增删改查。

### 常见的数据库管理系统：
	    
    MySQL、Oracle、MS SqlServer、DB2、sybase等....

### SQL：结构化查询语言
      
    程序员需要学习SQL语句，程序员通过编写SQL语句，然后DBMS负责执行SQL语句，最终来完成数据库中数据的增删改查操作。SQL是一套标准，程序员主要学习的就是SQL语句，这个SQL在mysql中可以使用，同时在Oracle中也可以使用，在DB2中也可以使用。

### DBMS SQl DB三者之间的关系？

    DBMS--执行--> SQL --操作--> DB


# 2、安装MySQL数据库管理系统。
	第一步：先安装，选择“经典版”
	第二步：需要进行MySQL数据库实例配置。
	注意：一路下一步就行了！！！！！

    
    字符编码方式？
	设置mysql数据库的字符编码方式为 UTF8
	一定要注意：先选中第3个单选按钮，然后再选择utf8字符集。
  
    服务名称默认是：MySQL.不用改。
		
      
    选择配置环境变量path：
	如果没有选择怎么办？你可以手动配置
	path=其它路径;C:\Program Files (x86)\MySQL\MySQL Server 5.5\bin
		
    mysql超级管理员用户名不能改，一定是：root
	你需要设置mysql数据库超级管理员的密码。
	我们设置为123456
	设置密码的同时，可以激活root账户远程访问。
	激活：表示root账号可以在外地登录。
	不激活：表示root账号只能在本机上使用。
	

# 3、MySQL数据库的完美卸载！
	第一步：双击安装包进行卸载删除。
	第二步：删除目录：
		把C:\ProgramData下面的MySQL目录干掉。
		把C:\Program Files (x86)下面的MySQL目录干掉。
	这样就卸载结束了！

# 4、看一下计算机上的服务，找一找MySQL的服务在哪里？
	计算机-->右键-->管理-->服务和应用程序-->服务-->找mysql服务
	MySQL的服务，默认是“启动”的状态，只有启动了mysql才能用。


# 5、在windows操作系统当中，怎么使用命令来启动和关闭mysql服务呢？
    net stop 服务名称; net start 服务名称;


# 6、mysql安装了，服务启动了，怎么使用客户端登录mysql数据库呢？
    -mysql -uroot -p123456
    -本地登录（隐藏密码的形式）：
    mysql -uroot -p
		

# 7、mysql常用命令：注意：以下命令不区分大小写，都行。
### 退出mysql ：
    exit

### 查看mysql中有哪些数据库.
    -show databases;  

### 怎么选择使用某个数据库呢？
    use xxx;

### 怎么创建数据库呢？
    create database xxx;

### 查看某个数据库下有哪些表？
    show tables;

### 查看mysql数据库的版本号：
    select version();

### 查看当前使用的是哪个数据库？
    select database();

### 如何建表
    create table 表名（字段名 字段类型（定义size）deafult '默认值'，字段名 字段类型）；
    eg: create table t_student(
		no int,
		name varchar(32),
		sex char(1) default 'm',
		age int(3),
		email varchar(255)
	);

### 删除表drop（DDL）：
		drop table t_student; // 当这张表不存在的时候会报错！
		// 如果这张表存在的话，删除
		drop table if exists t_student;

### 在mysql当中怎么获取系统当前时间？
		now() 函数，并且获取的时间带有：时分秒信息！！！！是datetime类型的。
		insert into t_user(id,name,birth,create_time) values(2,'lisi','1991-10-01',now());

### 修改update（DML）
    语法格式：update 表名 set 字段名1=值1,字段名2=值2,字段名3=值3... where 条件;
    注意：没有条件限制会导致所有数据全部更新。
### 删除数据 
    delete （DML）
    delete from 表名 where 条件;
    注意：没有条件，整张表的数据会全部删除！
         支持回滚
	delete from t_user where id = 2;
	delete from t_user; // 删除所有！


    truncate（DDl）
		这种删除效率比较高，表被一次截断，物理删除。
		这种删除缺点：不支持回滚。
		这种删除优点：快速。
    truncate table dept_bak; （这种操作属于DDL操作。）


### 如何插入数据insert （DML）
    insert into 表名(字段名1,字段名2,字段名3...) values(值1,值2,值3);
    eg1：insert into t_student(no,name,sex,age,email) values(1,'zhangsan','m',20,'zhangsan@123.com');
    eg2：insert into t_student(email,name,sex,age,no) values('lisi@123.com','lisi','f',20,2);  

    一次可以插入多条记录：
		insert into t_user(id,name,birth,create_time) values (1,'zs','1980-10-11',now()), (2,'lisi','1981-10-11',now()),(3,'wangwu','1982-10-11',now());

    -注意：字段名和值要一一对应。即数量要对应。数据类型要对应。  
    -注意：insert语句但凡是执行成功了，那么必然会多一条记录。没有给其它字段指定值的话，默认值是NULL  
    -注意：insert语句中的“字段名”可以省略   insert into t_student values(2); //错误的  
    -注意：前面的字段名省略的话，等于都写上了！所以值也要都写上！
		insert into t_student values(2, 'lisi', 'f', 20, 'lisi@123.com');



### insert插入日期
格式化数字：format(数字, '格式')

    select ename,format(sal, '$999,999') as sal from emp;  


将字符串varchar类型转换成date类型 mysql的日期格式：str_to_date：
    
    %Y年 %m月 %d 日%h	时%i 分%s	秒
    eg：类型不匹配。数据库birth是date类型，这里给了一个字符串varchar。
    insert into t_user(id,name,birth) values(1, 'zhangsan', '01-10-1990'); // 1990年10月1日
    应该是：
    insert into t_user(id,name,birth) values(1, 'zhangsan', str_to_date('01-10-1990','%d-%m-%Y'));  
date_format(日期类型数据, '日期格式')：将date类型转换成具有一定格式的varchar字符串类型  
    
    create table t_user(id int,name varchar(32),birth date // 生日也可以使用date日期类型);  
    create table t_user(id int,name varchar(32),birth char(10) // 生日可以使用字符串，没问题);  
查询的时候以某个特定的日期格式展示
    
    select id,name,date_format(birth, '%m/%d/%Y') as birth from t_user;  

怎么查看表中的数据呢
    
    select * from 表名; 

不看表中的数据，只看表的结构，有一个命令：
    
    desc 表名;

如何查询一个字段
  
  select 字段名 from 表名;

### 查询两个字段，或者多个字段怎么办
    使用逗号隔开 :select deptno,dname from dept

### 如何给查询的列起别名
    select deptno,dname as deptname from dept;
    注意：只是将显示的查询结果列名显示为deptname，原表列名还是叫：dname .as关键字可以省略：select deptno,dname deptname from dept;
### 假设起别名的时候，别名里面有空格，怎么办？
    select deptno,dname 'dept name' from dept; //加单引号  
    select deptno,dname "dept name" from dept; //加双引号  
    注意：在所有的数据库当中，字符串统一使用单引号括起来，单引号是标准，双引号在oracle数据库中用不了。但是在mysql中可以使用。再次强调：数据库中的字符串都是采用单引号括起来。这是标准的。双引号不标准。


### 如何进行条件查询
    select 字段1,字段2,字段3....from 表名 where 条件;
### 都有哪些条件
    = 等于  
    查询薪资等于800的员工姓名和编号？  
    select empno,ename from emp where sal = 800;  
    select empno,sal from emp where ename = 'SMITH'; //字符串使用单引号

    <>或!= 不等于  
    查询薪资不等于800的员工姓名和编号？  
    select empno,ename from emp where sal != 800;  
    select empno,ename from emp where sal <> 800; // 小于号和大于号组成的不等号

    < 小于  
    查询薪资小于2000的员工姓名和编号？  
    mysql> select empno,ename,sal from emp where sal < 2000;

    <= 小于等于  
    查询薪资小于等于3000的员工姓名和编号？  
    select empno,ename,sal from emp where sal <= 3000;

### between … and …. 两个值之间, 等同于 >= and <=
    查询薪资在2450和3000之间的员工信息？包括2450和3000  
    第一种方式：>= and <= （and是并且的意思。）
        select empno,ename,sal from emp where sal >= 2450 and sal <= 3000;  
    第二种方式：between … and …
          select 
    empno,ename,sal 
    from 
    emp   
    where 
    sal between 2450 and 3000;  
    注意：  
    1 使用between and的时候，必须遵循左小右大。  
    2 between and是闭区间，包括两端的值。

### 如何查询不为空-null的？
    在数据库当中null不能使用等号进行衡量。需要使用is null。因为数据库中的null代表什么也没有，它不是一个值，所以不能使用等号衡量。

### like：模糊查询，支持%或下划线匹配 %匹配任意多个字符 下划线：任意一个字符。

    找出名字中含有O的？
    mysql> select ename from emp where ename like '%O%';

    找出名字以T结尾的？
    select ename from emp where ename like '%T';
			
    找出名字以K开始的？
    select ename from emp where ename like 'K%';

    找出第二个字每是A的？
    select ename from emp where ename like '_A%';
		
    找出第三个字母是R的？
    select ename from emp where ename like '__R%';

    找出名字中有“_”的？
    select name from t_student where name like '%_%'; //这样不行
	  select name from t_student where name like '%\_%'; // \转义字符。

### 排序

    默认升序
    select ename,sal from emp order by sal; // 默认是升序！！！

    指定升序？
    select ename,sal from emp order by sal asc;

    降序？
    select ename,sal from emp order by sal desc;
	
    多个字段排序
	查询员工名字和薪资，要求按照薪资升序，如果薪资一样的话，再按照名字升序排列。
	select ename,sal from emp order by sal asc, ename asc; // sal在前，起主导，只有sal相等的时候，才会考虑启用ename排序。

    根据字段的位置也可以排序
	select ename,sal from emp order by 2; // 2表示第二列。第二列是sal
	按照查询结果的第2列sal排序。
	了解一下，不建议在开发中这样写，因为不健壮。
	因为列的顺序很容易发生改变，列顺序修改之后，2就废了。

### 把查询结果去除重复记录【distinct】
       select distinct job from emp;
       select distinct job,deptno from emp;
       注意：原表数据不会被修改，只是查询结果去重。去重需要使用一个关键字：distinct 
            distinct出现在job,deptno两个字段之前，表示两个字段联合起来去重。

### offset xx ：可用来做pagenation
    意思：从xx位起开始

### fetch xx row only：
    意思：只读前xx个
    
    


# sql练习题

### 计算员工年薪？sal * 12 
    select ename,sal*12 from emp; // 结论：字段可以使用数学表达式！  
    select ename,sal*12 as yearsal from emp; //起别名  
    select ename,sal*12 as '年薪' from emp; //别名是中文，用单引号括起来。

### 查询工作岗位是MANAGER并且工资大于2500的员工信息？
    select empno,ename,job,sal from emp where job = 'MANAGER' and sal > 2500;
		
### 查询工作岗位是MANAGER和SALESMAN的员工？
    select empno,ename,job from emp  where 	job = 'MANAGER' or job = 'SALESMAN';

### 找出工资大于2500并且部门编号为10的员工，或者20部门所有员工找出来
    select * from emp where sal > 2500 and deptno = 10 or deptno = 20;
    注意：and优先级比or高。以上语句会先执行and，然后执行or。

### 查询工资大于2500，并且部门编号为10或20部门的员工？
    select * from emp where sal > 2500 and (deptno = 10 or deptno = 20);
    注意：and和or同时出现，and优先级较高。如果想让or先执行，需要加“小括号”以后在开发中，如果不确定优先级，就加小括号就行了。

### in 包含，相当于多个 or （not in 不在这个范围中）

### 查询工作岗位是MANAGER和SALESMAN的员工？
    select empno,ename,job from emp where job = 'MANAGER' or job = 'SALESMAN';------->
	  select empno,ename,job from emp where job in('MANAGER', 'SALESMAN');
    注意：in不是一个区间。in后面跟的是具体的值。not in 表示不在这几个值当中的数据。
    select ename,sal from emp where sal not in(800, 5000, 3000);  
    not 可以取非，主要用在 is 或 in 中  
    is null
    is not null
    in
    not in

### 综合一点的案例：
	找出工资在1250到3000之间的员工信息，要求按照薪资降序排列。
	select ename,sal from emp where sal between 1250 and 3000 order by sal desc;
	关键字顺序不能变，必须掌握：
	  第一步：from
		第二步：where
		第三步：select
		第四步：order by（排序总是在最后执行！）
### 找出每个工作岗位的工资和？
	
		实现思路：按照工作岗位分组，然后对工资求和。
			select 
				job,sum(sal)
			from
				emp
			group by
				job;
			
			+-----------+----------+
			| job       | sum(sal) |
			+-----------+----------+
			| ANALYST   |  6000.00 |
			| CLERK     |  4150.00 |
			| MANAGER   |  8275.00 |
			| PRESIDENT |  5000.00 |
			| SALESMAN  |  5600.00 |
			+-----------+----------+
			以上这个语句的执行顺序？
				先从emp表中查询数据。
				根据job字段进行分组。
				然后对每一组的数据进行sum(sal)
		
		select ename,job,sum(sal) from emp group by job;
		+-------+-----------+----------+
		| ename | job       | sum(sal) |
		+-------+-----------+----------+
		| SCOTT | ANALYST   |  6000.00 |
		| SMITH | CLERK     |  4150.00 |
		| JONES | MANAGER   |  8275.00 |
		| KING  | PRESIDENT |  5000.00 |
		| ALLEN | SALESMAN  |  5600.00 |
		+-------+-----------+----------+
		以上语句在mysql中可以执行，但是毫无意义。
		以上语句在oracle中执行报错。
		oracle的语法比mysql的语法严格。（mysql的语法相对来说松散一些！）

		重点结论：
			在一条select语句当中，如果有group by语句的话，
			select后面只能跟：参加分组的字段，以及分组函数。
			其它的一律不能跟。

### 找出每个部门的最高薪资
		实现思路是什么？
			按照部门编号分组，求每一组的最大值。

			select后面添加ename字段没有意义，另外oracle会报错。
			mysql> select ename,deptno,max(sal) from emp group by deptno;
			+-------+--------+----------+
			| ename | deptno | max(sal) |
			+-------+--------+----------+
			| CLARK |     10 |  5000.00 |
			| SMITH |     20 |  3000.00 |
			| ALLEN |     30 |  2850.00 |
			+-------+--------+----------+

			mysql> select deptno,max(sal) from emp group by deptno;
			+--------+----------+
			| deptno | max(sal) |
			+--------+----------+
			|     10 |  5000.00 |
			|     20 |  3000.00 |
			|     30 |  2850.00 |
			+--------+----------+

### 找出“每个部门，不同工作岗位”的最高薪资？
		+--------+-----------+---------+--------+
		| ename  | job       | sal     | deptno |
		+--------+-----------+---------+--------+
		| MILLER | CLERK     | 1300.00 |     10 |
		| KING   | PRESIDENT | 5000.00 |     10 |
		| CLARK  | MANAGER   | 2450.00 |     10 |

		| FORD   | ANALYST   | 3000.00 |     20 |
		| ADAMS  | CLERK     | 1100.00 |     20 |
		| SCOTT  | ANALYST   | 3000.00 |     20 |
		| JONES  | MANAGER   | 2975.00 |     20 |
		| SMITH  | CLERK     |  800.00 |     20 |

		| BLAKE  | MANAGER   | 2850.00 |     30 |
		| MARTIN | SALESMAN  | 1250.00 |     30 |
		| ALLEN  | SALESMAN  | 1600.00 |     30 |
		| TURNER | SALESMAN  | 1500.00 |     30 |
		| WARD   | SALESMAN  | 1250.00 |     30 |
		| JAMES  | CLERK     |  950.00 |     30 |
		+--------+-----------+---------+--------+
		技巧：两个字段联合成1个字段看。（两个字段联合分组）
		select 
			deptno, job, max(sal)
		from
			emp
		group by
			deptno, job;

		+--------+-----------+----------+
		| deptno | job       | max(sal) |
		+--------+-----------+----------+
		|     10 | CLERK     |  1300.00 |
		|     10 | MANAGER   |  2450.00 |
		|     10 | PRESIDENT |  5000.00 |
		|     20 | ANALYST   |  3000.00 |
		|     20 | CLERK     |  1100.00 |
		|     20 | MANAGER   |  2975.00 |
		|     30 | CLERK     |   950.00 |
		|     30 | MANAGER   |  2850.00 |
		|     30 | SALESMAN  |  1600.00 |
		+--------+-----------+----------+
		
### 使用having可以对分完组之后的数据进一步过滤。
	having不能单独使用，having不能代替where，having必须
	和group by联合使用。

### 找出每个部门最高薪资，要求显示最高薪资大于3000的？

		第一步：找出每个部门最高薪资
			按照部门编号分组，求每一组最大值。
			select deptno,max(sal) from emp group by deptno;
			+--------+----------+
			| deptno | max(sal) |
			+--------+----------+
			|     10 |  5000.00 |
			|     20 |  3000.00 |
			|     30 |  2850.00 |
			+--------+----------+
		
		第二步：要求显示最高薪资大于3000
			select 
				deptno,max(sal) 
			from 
				emp 
			group by 
				deptno
			having
				max(sal) > 3000;

			+--------+----------+
			| deptno | max(sal) |
			+--------+----------+
			|     10 |  5000.00 |
			+--------+----------+


			思考一个问题：以上的sql语句执行效率是不是低？
			比较低，实际上可以这样考虑：先将大于3000的都找出来，然后再分组。
			select 
				deptno,max(sal)
			from
				emp
			where
				sal > 3000
			group by
				deptno;
			
			+--------+----------+
			| deptno | max(sal) |
			+--------+----------+
			|     10 |  5000.00 |
			+--------+----------+

			优化策略：
				where和having，优先选择where，where实在完成不了了，再选择
				having。
		
### where没办法的？？？？
			找出每个部门平均薪资，要求显示平均薪资高于2500的。

			第一步：找出每个部门平均薪资
				select deptno,avg(sal) from emp group by deptno;
				+--------+-------------+
				| deptno | avg(sal)    |
				+--------+-------------+
				|     10 | 2916.666667 |
				|     20 | 2175.000000 |
				|     30 | 1566.666667 |
				+--------+-------------+

			第二步：要求显示平均薪资高于2500的
				select 
					deptno,avg(sal) 
				from 
					emp 
				group by 
					deptno
				having
					avg(sal) > 2500;
			
			+--------+-------------+
			| deptno | avg(sal)    |
			+--------+-------------+
			|     10 | 2916.666667 |
			+--------+-------------+

# 8、数据处理函数（单行处理函数）
### 单行处理函数 
    特点：
    1 一个输入对应一个输出。 
    select lower(ename) as ename from emp;
		+--------+
		| ename  |
		+--------+
		| smith  |
		| allen  |
		| ward   |
		| jones  |
		| martin |
		| blake  |
		| clark  |
		| scott  |
		| king   |
		| turner |
		| adams  |
		| james  |
		| ford   |
		| miller |
		+--------+
    14个输入，最后还是14个输出。这是单行处理函数的特点。  
    2 函数名加小括号
    
    dan处理函数常见的有哪些
    1. lower 转换小写 
    2. upper 转换大写
       select upper(name) as name from t_student;
    3. substr 取子串（substr( 被截取的字符串, 起始下标,截取的长度)）
       select substr(ename, 1, 1) as ename from emp;
		注意：起始下标从1开始，没有0.
		找出员工名字第一个字母是A的员工信息？
		第一种方式：模糊查询
				select ename from emp where ename like 'A%';
		第二种方式：substr函数
				select ename from emp where substr(ename,1,1) = 'A';
    4. concat函数进行字符串的拼接
		select concat(empno,ename) from emp;
		+---------------------+
		| concat(empno,ename) |
		+---------------------+
		| 7369SMITH           |
		| 7499ALLEN           |
		| 7521WARD            |
	
    5. length 取长度
      select length(ename) enamelength from emp;
    6 trim 去空格
	   select * from emp where ename = trim('   KING');
    7. str_to_date 将字符串转换成日期
    8. date_format 格式化日期
    9. format 设置千分位
    10. case..when..then..when..then..else..end
        当员工的工作岗位是MANAGER的时候，工资上调10%，  
        当工作岗位是SALESMAN的时候，工资上调50%,其它正常。
       （注意：不修改数据库，只是将查询结果显示为工资上调）
        select ename,job, sal as oldsal,(case job when 'MANAGER' then sal*1.1 when 'SALESMAN' then sal*1.5 else sal end) as newsal from emp;
		
		+--------+-----------+---------+---------+
		| ename  | job       | oldsal  | newsal  |
		+--------+-----------+---------+---------+
		| SMITH  | CLERK     |  800.00 |  800.00 |
		| ALLEN  | SALESMAN  | 1600.00 | 2400.00 |
		| WARD   | SALESMAN  | 1250.00 | 1875.00 |
		| JONES  | MANAGER   | 2975.00 | 3272.50 |
		| MARTIN | SALESMAN  | 1250.00 | 1875.00 |
		| BLAKE  | MANAGER   | 2850.00 | 3135.00 |
		| CLARK  | MANAGER   | 2450.00 | 2695.00 |
		| SCOTT  | ANALYST   | 3000.00 | 3000.00 |
		| KING   | PRESIDENT | 5000.00 | 5000.00 |
		| TURNER | SALESMAN  | 1500.00 | 2250.00 |
		| ADAMS  | CLERK     | 1100.00 | 1100.00 |
		| JAMES  | CLERK     |  950.00 |  950.00 |
		| FORD   | ANALYST   | 3000.00 | 3000.00 |
		| MILLER | CLERK     | 1300.00 | 1300.00 |
		+--------+-----------+---------+---------+
    11. round 四舍五入
        select round(1236.567, 0) as result from emp; //保留整数位
		select round(1236.567, 1) as result from emp; //保留1个小数
		select round(1236.567, 2) as result from emp; //保留2个小数
		select round(1236.567, -1) as result from emp; // 保留到十位。
    12. select 'abc' from emp; // select后面直接跟“字面量/字面值” 会根据表结构生成相应量 例如下面的名字字段中有14个值  这样输入会生成14个值
    select 'abc' as bieming from emp;
		+---------+
		| bieming |
		+---------+
		| abc     |
		| abc     |
		| abc     |
		| abc     |
		| abc     |
		| abc     |
		| abc     |
		| abc     |
		| abc     |
		| abc     |
		| abc     |
		| abc     |
		| abc     |
		| abc     |
		+---------+
		mysql> select abc from emp;
		ERROR 1054 (42S22): Unknown column 'abc' in 'field list'
		这样肯定报错，因为会把abc当做一个字段的名字，去emp表中找abc字段去了。

		select 1000 as num from emp; // 1000 也是被当做一个字面量/字面值。
		+------+
		| num  |
		+------+
		| 1000 |
		| 1000 |
		| 1000 |
		| 1000 |
		| 1000 |
		| 1000 |
		| 1000 |
		| 1000 |
		| 1000 |
		| 1000 |
		| 1000 |
		| 1000 |
		| 1000 |
		| 1000 |
		+------+

		结论：select后面可以跟某个表的字段名（可以等同看做变量名），也可以跟字面量/字面值（数据）。
		select 21000 as num from dept;
		+-------+
		| num   |
		+-------+
		| 21000 |
		| 21000 |
		| 21000 |
		| 21000 |
		+-------+
    13. rand() 生成随机数
		mysql> select round(rand()*100,0) from emp; // 100以内的随机数
    14. ifnull 可以将 null 转换成一个具体值 注意：NULL只要参与运算，最终结果一定是NULL。为了避免这个现象，需要使用ifnull函数。
    ifnull函数用法：ifnull(数据, 被当做哪个值) 如果“数据”为NULL的时候，把这个数据结构当做哪个值。ifnull是空处理函数。专门处理空的。在所有数据库当中，只要有NULL参与的数学运算，最终结果就是NULL
    补助为NULL的时候，将补助当做0
    select ename, (sal + ifnull(comm, 0)) * 12 as yearsal from emp;
				+--------+----------+
				| ename  | yearsal  |
				+--------+----------+
				| SMITH  |  9600.00 |
				| ALLEN  | 22800.00 |
				| WARD   | 21000.00 |
				| JONES  | 35700.00 |
				| MARTIN | 31800.00 |
				| BLAKE  | 34200.00 |
				| CLARK  | 29400.00 |
				| SCOTT  | 36000.00 |
				| KING   | 60000.00 |
				| TURNER | 18000.00 |
				| ADAMS  | 13200.00 |
				| JAMES  | 11400.00 |
				| FORD   | 36000.00 |
				| MILLER | 15600.00 |
				+--------+----------+

		

### 多行处理函数 
    特点
    多个输入，对应1个输出

    多处理函数常见的有哪些
    
    分组函数（多行处理函数）注意：分组函数在使用的时候必须先进行分组，然后才能用。如果你没有对数据进行分组，整张表默认为一组。
	
	找出最高工资？
		mysql> select max(sal) from emp;
		+----------+
		| max(sal) |
		+----------+
		|  5000.00 |
		+----------+
	
	找出最低工资？
		mysql> select min(sal) from emp;
		+----------+
		| min(sal) |
		+----------+
		|   800.00 |
		+----------+
	
	计算工资和：
		mysql> select sum(sal) from emp;
		+----------+
		| sum(sal) |
		+----------+
		| 29025.00 |
		+----------+
	
	计算平均工资：
		mysql> select avg(sal) from emp;
		+-------------+
		| avg(sal)    |
		+-------------+
		| 2073.214286 |
		+-------------+
		14个工资全部加起来，然后除以14。
	
	计算员工数量？
		mysql> select count(ename) from emp;
		+--------------+
		| count(ename) |
		+--------------+
		|           14 |
		+--------------+
	
	分组函数在使用的时候需要注意哪些？

		第一点：分组函数自动忽略NULL，你不需要提前对NULL进行处理。
		第二点：分组函数中count(*)和count(具体字段)有什么区别
			count(具体字段)：表示统计该字段下所有不为NULL的元素的总数。
			count(*)：统计表当中的总行数。（只要有一行数据count则++）因为每一行记录不可能都为NULL，一行数据中有一列不为NULL，则这行数据就是有效的。
		第三点：分组函数不能够直接使用在where子句中。
			找出比最低工资高的员工信息。
			select ename,sal from emp where sal > min(sal);
			表面上没问题，运行一下？
			ERROR 1111 (HY000): Invalid use of group function
			说完分组查询(group by)之后就明白了了。
		第四点：所有的分组函数可以组合起来一起用。
			select sum(sal),min(sal),max(sal),avg(sal),count(*) from emp;
			+----------+----------+----------+-------------+----------+
			| sum(sal) | min(sal) | max(sal) | avg(sal)    | count(*) |
			+----------+----------+----------+-------------+----------+
			| 29025.00 |   800.00 |  5000.00 | 2073.214286 |       14 |
			+----------+----------+----------+-------------+----------+

# 9、分组查询（非常重要：五颗星*****）
### 什么是分组查询？
    在实际的应用中，可能有这样的需求，需要先进行分组，然后对每一组的数据进行操作。
    这个时候我们需要使用分组查询，怎么进行分组查询呢？
	举个例子，如果你想查询一个表中每个省份的人口总数，你可以使用GROUP BY 子句来按省份分组，然后使用COUNT函数计算每个省份的人口总数：
    SELECT province, COUNT(*) AS population FROM people GROUP BY province;
			....
	将之前的关键字全部组合在一起，来看一下他们的执行顺序？
		select
			...
		from
			...
		where
			...
		group by
			...
		order by
			...
		
    以上关键字的顺序不能颠倒，需要记忆。执行顺序：
			1. from
			2. where
			3. group by
			4. select
			5. order by
		
### 为什么分组函数不能直接使用在where后面？
			select ename,sal from emp where sal > min(sal);//报错。
			因为分组函数在使用的时候必须先分组之后才能使用。
			where执行的时候，还没有分组。所以where后面不能出现分组函数。

			select sum(sal) from emp; 
			这个没有分组，为啥sum()函数可以用呢？
				因为select在group by之后执行。
			
	

# 10、大总结（单表的查询）
	从某张表中查询数据，
	先经过where条件筛选出有价值的数据。
	对这些有价值的数据进行分组。
	分组之后可以使用having继续筛选。
	select查询出来。
	最后排序输出！

	每一个字段都有：字段名、数据类型、约束等属性。
	字段名可以理解，是一个普通的名字，见名知意就行。
	数据类型：字符串，数字，日期等，后期讲。

	约束：约束也有很多，其中一个叫做唯一性约束，这种约束添加之后，该字段中的数据不能重复。


# 11、SQL语句的分类
    DQL：
            数据查询语言（凡是带有select关键字的都是查询语句）
            select...

    DML：
            数据操作语言（凡是对表当中的数据进行增删改的都是DML）
            insert delete update
            insert 增
            delete 删
            update 改

            这个主要是操作表中的数据data。

    DDL：
            数据定义语言
            凡是带有create、drop、alter的都是DDL。
            DDL主要操作的是表的结构。不是表中的数据。
            create：新建，等同于增
            drop：删除
            alter：修改
            这个增删改和DML不同，这个主要是对表结构进行操作。

    TCL：
            不是王牌电视。
            是事务控制语言
            包括：
              事务提交：commit;
              事务回滚：rollback;

    DCL：
            是数据控制语言。
            例如：授权grant、撤销权限revoke....


# 12、导入一下提前准备好的数据：
    source D:\course\03-MySQL\document\bjpowernode.sql
    注意： 1 这里source 的时候要先进入！！！！！即use！！！！！！
          2 记住要把\变成/！ ！！！！！
          3 路径中不要有中文！！！！





# 13、 连接查询

### 什么是连接查询？
	从一张表中单独查询，称为单表查询。emp表和dept表联合起来查询数据，从emp表中取员工名字，从dept表中取部门名字。这种跨表查询，多张表联合起来查询数据，被称为连接查询。

### 连接查询的分类？
		内连接：
			等值连接
			非等值连接
			自连接

		外连接：
			左外连接（左连接）
			右外连接（右连接）

		全连接（不讲）

### 当两张表进行连接查询时，没有任何条件的限制会发生什么现象？

	案例：查询每个员工所在部门名称？
		mysql> select ename,deptno from emp;
		+--------+--------+
		| ename  | deptno |
		+--------+--------+
		| SMITH  |     20 |
		| ALLEN  |     30 |
		| WARD   |     30 |
		| JONES  |     20 |
		| MARTIN |     30 |
		| BLAKE  |     30 |
		| CLARK  |     10 |
		| SCOTT  |     20 |
		| KING   |     10 |
		| TURNER |     30 |
		| ADAMS  |     20 |
		| JAMES  |     30 |
		| FORD   |     20 |
		| MILLER |     10 |
		+--------+--------+
		mysql> select * from dept;
		+--------+------------+----------+
		| DEPTNO | DNAME      | LOC      |
		+--------+------------+----------+
		|     10 | ACCOUNTING | NEW YORK |
		|     20 | RESEARCH   | DALLAS   |
		|     30 | SALES      | CHICAGO  |
		|     40 | OPERATIONS | BOSTON   |
		+--------+------------+----------+

		两张表连接没有任何条件限制：
		select ename,dname from emp, dept;
		+--------+------------+
		| ename  | dname      |
		+--------+------------+
		| SMITH  | ACCOUNTING |
		| SMITH  | RESEARCH   |
		| SMITH  | SALES      |
		| SMITH  | OPERATIONS |
		| ALLEN  | ACCOUNTING |
		| ALLEN  | RESEARCH   |
		| ALLEN  | SALES      |
		| ALLEN  | OPERATIONS |
		...
		56 rows in set (0.00 sec)
		14 * 4 = 56

		当两张表进行连接查询，没有任何条件限制的时候，最终查询结果条数，是
		两张表条数的乘积，这种现象被称为：笛卡尔积现象。（笛卡尔发现的，这是
		一个数学现象。）

### 怎么避免笛卡尔积现象？
	连接时加条件，满足这个条件的记录被筛选出来！
	select ename,dname from emp, dept where emp.deptno = dept.deptno;  
    select emp.ename,dept.dname from  emp, dep where emp.deptno = dept.deptno;

	思考：最终查询的结果条数是14条，但是匹配的过程中，匹配的次数减少了吗？
		还是56次，只不过进行了四选一。次数没有减少。
	
	注意：通过笛卡尔积现象得出，表的连接次数越多效率越低，尽量避免表的连接次数。

### 内连接之等值连接。

    案例：查询每个员工所在部门名称，显示员工名和部门名？emp e和dept d表进行连接。条件是：e.deptno = d.deptno

	//inner可以省略（带着inner可读性更好！！！一眼就能看出来是内连接）
	select 
		e.ename,d.dname
	from
		emp e
	inner join
		dept d
	on
		e.deptno = d.deptno; // 条件是等量关系，所以被称为等值连接。



### 内连接之非等值连接

    案例：找出每个员工的薪资等级，要求显示员工名、薪资、薪资等级

    select 
      e.ename, e.sal, s.grade
    from
      emp e
    join
      salgrade s
    on
      e.sal between s.losal and s.hisal; // 条件不是一个等量关系，称为非等值连接。

### 内连接之自连接
    案例：查询员工的上级领导，要求显示员工名和对应的领导名？
    select empno,ename,mgr from emp;
    +-------+--------+------+
    | empno | ename  | mgr  |
    +-------+--------+------+
    |  7369 | SMITH  | 7902 |
    |  7499 | ALLEN  | 7698 |
    |  7521 | WARD   | 7698 |
    |  7566 | JONES  | 7839 |
    |  7654 | MARTIN | 7698 |
    |  7698 | BLAKE  | 7839 |
    |  7782 | CLARK  | 7839 |
    |  7788 | SCOTT  | 7566 |
    |  7839 | KING   | NULL |
    |  7844 | TURNER | 7698 |
    |  7876 | ADAMS  | 7788 |
    |  7900 | JAMES  | 7698 |
    |  7902 | FORD   | 7566 |
    |  7934 | MILLER | 7782 |
    +-------+--------+------+

    技巧：一张表看成两张表。
    emp a 员工表
    +-------+--------+------+
    | empno | ename  | mgr  |
    +-------+--------+------+
    |  7369 | SMITH  | 7902 |
    |  7499 | ALLEN  | 7698 |
    |  7521 | WARD   | 7698 |
    |  7566 | JONES  | 7839 |
    |  7654 | MARTIN | 7698 |
    |  7698 | BLAKE  | 7839 |
    |  7782 | CLARK  | 7839 |
    |  7788 | SCOTT  | 7566 |
    |  7839 | KING   | NULL |
    |  7844 | TURNER | 7698 |
    |  7876 | ADAMS  | 7788 |
    |  7900 | JAMES  | 7698 |
    |  7902 | FORD   | 7566 |
    |  7934 | MILLER | 7782 |
    +-------+--------+------+

    emp b 领导表
    +-------+--------+------+
    | empno | ename  | mgr  |
    +-------+--------+------+
    |  7369 | SMITH  | 7902 |
    |  7499 | ALLEN  | 7698 |
    |  7521 | WARD   | 7698 |
    |  7566 | JONES  | 7839 |
    |  7654 | MARTIN | 7698 |
    |  7698 | BLAKE  | 7839 |
    |  7782 | CLARK  | 7839 |
    |  7788 | SCOTT  | 7566 |
    |  7839 | KING   | NULL |
    |  7844 | TURNER | 7698 |
    |  7876 | ADAMS  | 7788 |
    |  7900 | JAMES  | 7698 |
    |  7902 | FORD   | 7566 |
    |  7934 | MILLER | 7782 |
    +-------+--------+------+

    select 
      a.ename as '员工名', b.ename as '领导名'
    from
      emp a
    join
      emp b
    on
      a.mgr = b.empno; //员工的领导编号 = 领导的员工编号

    +--------+--------+
    | 员工名 | 领导名|
    +--------+--------+
    | SMITH  | FORD   |
    | ALLEN  | BLAKE  |
    | WARD   | BLAKE  |
    | JONES  | KING   |
    | MARTIN | BLAKE  |
    | BLAKE  | KING   |
    | CLARK  | KING   |
    | SCOTT  | JONES  |
    | TURNER | BLAKE  |
    | ADAMS  | SCOTT  |
    | JAMES  | BLAKE  |
    | FORD   | JONES  |
    | MILLER | CLARK  |
    +--------+--------+
    13条记录，没有KING。《内连接》

    以上就是内连接中的：自连接，技巧：一张表看做两张表。

### 外连接

    select * from emp; e
    +-------+--------+-----------+------+------------+---------+---------+--------+
    | EMPNO | ENAME  | JOB       | MGR  | HIREDATE   | SAL     | COMM    | DEPTNO |
    +-------+--------+-----------+------+------------+---------+---------+--------+
    |  7369 | SMITH  | CLERK     | 7902 | 1980-12-17 |  800.00 |    NULL |     20 |
    |  7499 | ALLEN  | SALESMAN  | 7698 | 1981-02-20 | 1600.00 |  300.00 |     30 |
    |  7521 | WARD   | SALESMAN  | 7698 | 1981-02-22 | 1250.00 |  500.00 |     30 |
    |  7566 | JONES  | MANAGER   | 7839 | 1981-04-02 | 2975.00 |    NULL |     20 |
    |  7654 | MARTIN | SALESMAN  | 7698 | 1981-09-28 | 1250.00 | 1400.00 |     30 |
    |  7698 | BLAKE  | MANAGER   | 7839 | 1981-05-01 | 2850.00 |    NULL |     30 |
    |  7782 | CLARK  | MANAGER   | 7839 | 1981-06-09 | 2450.00 |    NULL |     10 |
    |  7788 | SCOTT  | ANALYST   | 7566 | 1987-04-19 | 3000.00 |    NULL |     20 |
    |  7839 | KING   | PRESIDENT | NULL | 1981-11-17 | 5000.00 |    NULL |     10 |
    |  7844 | TURNER | SALESMAN  | 7698 | 1981-09-08 | 1500.00 |    0.00 |     30 |
    |  7876 | ADAMS  | CLERK     | 7788 | 1987-05-23 | 1100.00 |    NULL |     20 |
    |  7900 | JAMES  | CLERK     | 7698 | 1981-12-03 |  950.00 |    NULL |     30 |
    |  7902 | FORD   | ANALYST   | 7566 | 1981-12-03 | 3000.00 |    NULL |     20 |
    |  7934 | MILLER | CLERK     | 7782 | 1982-01-23 | 1300.00 |    NULL |     10 |
    +-------+--------+-----------+------+------------+---------+---------+--------+

    mysql> select * from dept; d
    +--------+------------+----------+
    | DEPTNO | DNAME      | LOC      |
    +--------+------------+----------+
    |     10 | ACCOUNTING | NEW YORK |
    |     20 | RESEARCH   | DALLAS   |
    |     30 | SALES      | CHICAGO  |
    |     40 | OPERATIONS | BOSTON   |
    +--------+------------+----------+

    内连接：（A和B连接，AB两张表没有主次关系。平等的。）
    select 
      e.ename,d.dname
    from
      emp e
    join
      dept d
    on
      e.deptno = d.deptno; //内连接的特点：完成能够匹配上这个条件的数据查询出来。

    +--------+------------+
    | ename  | dname      |
    +--------+------------+
    | CLARK  | ACCOUNTING |
    | KING   | ACCOUNTING |
    | MILLER | ACCOUNTING |
    | SMITH  | RESEARCH   |
    | JONES  | RESEARCH   |
    | SCOTT  | RESEARCH   |
    | ADAMS  | RESEARCH   |
    | FORD   | RESEARCH   |
    | ALLEN  | SALES      |
    | WARD   | SALES      |
    | MARTIN | SALES      |
    | BLAKE  | SALES      |
    | TURNER | SALES      |
    | JAMES  | SALES      |
    +--------+------------+

    外连接（右外连接）：
    select 
      e.ename,d.dname
    from
      emp e 
    right join 
      dept d
    on
      e.deptno = d.deptno;

    // outer是可以省略的，带着可读性强。
    select 
      e.ename,d.dname
    from
      emp e 
    right outer join 
      dept d
    on
      e.deptno = d.deptno;

    right代表什么：表示将join关键字右边的这张表看成主表，主要是为了将
    这张表的数据全部查询出来，捎带着关联查询左边的表。
    在外连接当中，两张表连接，产生了主次关系。

    外连接（左外连接）：
    select 
      e.ename,d.dname
    from
      dept d 
    left join 
      emp e
    on
      e.deptno = d.deptno;

    // outer是可以省略的，带着可读性强。
    select 
      e.ename,d.dname
    from
      dept d 
    left outer join 
      emp e
    on
      e.deptno = d.deptno;

    带有right的是右外连接，又叫做右连接。
    带有left的是左外连接，又叫做左连接。
    任何一个右连接都有左连接的写法。
    任何一个左连接都有右连接的写法。

    +--------+------------+
    | ename  | dname      |
    +--------+------------+
    | CLARK  | ACCOUNTING |
    | KING   | ACCOUNTING |
    | MILLER | ACCOUNTING |
    | SMITH  | RESEARCH   |
    | JONES  | RESEARCH   |
    | SCOTT  | RESEARCH   |
    | ADAMS  | RESEARCH   |
    | FORD   | RESEARCH   |
    | ALLEN  | SALES      |
    | WARD   | SALES      |
    | MARTIN | SALES      |
    | BLAKE  | SALES      |
    | TURNER | SALES      |
    | JAMES  | SALES      |
    | NULL   | OPERATIONS |
    +--------+------------+

    思考：外连接的查询结果条数一定是 >= 内连接的查询结果条数？
      正确。


    案例：查询每个员工的上级领导，要求显示所有员工的名字和领导名？
      select 
        a.ename as '员工名', b.ename as '领导名'
      from
        emp a
      left join
        emp b
      on
        a.mgr = b.empno; 
      
      +--------+--------+
      | 员工名      | 领导名     |
      +--------+--------+
      | SMITH  | FORD   |
      | ALLEN  | BLAKE  |
      | WARD   | BLAKE  |
      | JONES  | KING   |
      | MARTIN | BLAKE  |
      | BLAKE  | KING   |
      | CLARK  | KING   |
      | SCOTT  | JONES  |
      | KING   | NULL   |
      | TURNER | BLAKE  |
      | ADAMS  | SCOTT  |
      | JAMES  | BLAKE  |
      | FORD   | JONES  |
      | MILLER | CLARK  |
      +--------+--------+


### 三张表，四张表怎么连接？
	语法：
		select 
			...
		from
			a
		join
			b
		on
			a和b的连接条件
		join
			c
		on
			a和c的连接条件
		right join
			d
		on
			a和d的连接条件
		
		一条SQL中内连接和外连接可以混合。都可以出现！

	案例：找出每个员工的部门名称以及工资等级，
	要求显示员工名、部门名、薪资、薪资等级？
	
	select 
		e.ename,e.sal,d.dname,s.grade
	from
		emp e
	join
		dept d
	on 
		e.deptno = d.deptno
	join
		salgrade s
	on
		e.sal between s.losal and s.hisal;
	
	+--------+---------+------------+-------+
	| ename  | sal     | dname      | grade |
	+--------+---------+------------+-------+
	| SMITH  |  800.00 | RESEARCH   |     1 |
	| ALLEN  | 1600.00 | SALES      |     3 |
	| WARD   | 1250.00 | SALES      |     2 |
	| JONES  | 2975.00 | RESEARCH   |     4 |
	| MARTIN | 1250.00 | SALES      |     2 |
	| BLAKE  | 2850.00 | SALES      |     4 |
	| CLARK  | 2450.00 | ACCOUNTING |     4 |
	| SCOTT  | 3000.00 | RESEARCH   |     4 |
	| KING   | 5000.00 | ACCOUNTING |     5 |
	| TURNER | 1500.00 | SALES      |     3 |
	| ADAMS  | 1100.00 | RESEARCH   |     1 |
	| JAMES  |  950.00 | SALES      |     1 |
	| FORD   | 3000.00 | RESEARCH   |     4 |
	| MILLER | 1300.00 | ACCOUNTING |     2 |
	+--------+---------+------------+-------+

	案例：找出每个员工的部门名称以及工资等级，还有上级领导，
	要求显示员工名、领导名、部门名、薪资、薪资等级？

	select 
		e.ename,e.sal,d.dname,s.grade,l.ename
	from
		emp e
	join
		dept d
	on 
		e.deptno = d.deptno
	join
		salgrade s
	on
		e.sal between s.losal and s.hisal
	left join
		emp l
	on
		e.mgr = l.empno;
	
	+--------+---------+------------+-------+-------+
	| ename  | sal     | dname      | grade | ename |
	+--------+---------+------------+-------+-------+
	| SMITH  |  800.00 | RESEARCH   |     1 | FORD  |
	| ALLEN  | 1600.00 | SALES      |     3 | BLAKE |
	| WARD   | 1250.00 | SALES      |     2 | BLAKE |
	| JONES  | 2975.00 | RESEARCH   |     4 | KING  |
	| MARTIN | 1250.00 | SALES      |     2 | BLAKE |
	| BLAKE  | 2850.00 | SALES      |     4 | KING  |
	| CLARK  | 2450.00 | ACCOUNTING |     4 | KING  |
	| SCOTT  | 3000.00 | RESEARCH   |     4 | JONES |
	| KING   | 5000.00 | ACCOUNTING |     5 | NULL  |
	| TURNER | 1500.00 | SALES      |     3 | BLAKE |
	| ADAMS  | 1100.00 | RESEARCH   |     1 | SCOTT |
	| JAMES  |  950.00 | SALES      |     1 | BLAKE |
	| FORD   | 3000.00 | RESEARCH   |     4 | JONES |
	| MILLER | 1300.00 | ACCOUNTING |     2 | CLARK |
	+--------+---------+------------+-------+-------+

# 14 子查询？

3.1、什么是子查询？
	select语句中嵌套select语句，被嵌套的select语句称为子查询。

3.2、子查询都可以出现在哪里呢？
	select
		..(select).
	from
		..(select).
	where
		..(select).

3.3、where子句中的子查询

	案例：找出比最低工资高的员工姓名和工资？
		select 
			ename,sal
		from
			emp 
		where
			sal > min(sal);

		ERROR 1111 (HY000): Invalid use of group function
		where子句中不能直接使用分组函数。
	
	实现思路：
		第一步：查询最低工资是多少
			select min(sal) from emp;
			+----------+
			| min(sal) |
			+----------+
			|   800.00 |
			+----------+
		第二步：找出>800的
			select ename,sal from emp where sal > 800;
		
		第三步：合并
			select ename,sal from emp where sal > (select min(sal) from emp);
			+--------+---------+
			| ename  | sal     |
			+--------+---------+
			| ALLEN  | 1600.00 |
			| WARD   | 1250.00 |-
			| JONES  | 2975.00 |
			| MARTIN | 1250.00 |
			| BLAKE  | 2850.00 |
			| CLARK  | 2450.00 |
			| SCOTT  | 3000.00 |
			| KING   | 5000.00 |
			| TURNER | 1500.00 |
			| ADAMS  | 1100.00 |
			| JAMES  |  950.00 |
			| FORD   | 3000.00 |
			| MILLER | 1300.00 |
			+--------+---------+

3.4、from子句中的子查询
	注意：from后面的子查询，可以将子查询的查询结果当做一张临时表。（技巧）

	案例：找出每个岗位的平均工资的薪资等级。

	第一步：找出每个岗位的平均工资（按照岗位分组求平均值）
		select job,avg(sal) from emp group by job;
		+-----------+-------------+
		| job       | avgsal      |
		+-----------+-------------+
		| ANALYST   | 3000.000000 |
		| CLERK     | 1037.500000 |
		| MANAGER   | 2758.333333 |
		| PRESIDENT | 5000.000000 |
		| SALESMAN  | 1400.000000 |
		+-----------+-------------+t表

	第二步：克服心理障碍，把以上的查询结果就当做一张真实存在的表t。
	mysql> select * from salgrade; s表
	+-------+-------+-------+
	| GRADE | LOSAL | HISAL |
	+-------+-------+-------+
	|     1 |   700 |  1200 |
	|     2 |  1201 |  1400 |
	|     3 |  1401 |  2000 |
	|     4 |  2001 |  3000 |
	|     5 |  3001 |  9999 |
	+-------+-------+-------+
	t表和s表进行表连接，条件：t表avg(sal) between s.losal and s.hisal;
		
		select 
			t.*, s.grade
		from
			(select job,avg(sal) as avgsal from emp group by job) t
		join
			salgrade s
		on
			t.avgsal between s.losal and s.hisal;
		
		+-----------+-------------+-------+
		| job       | avgsal      | grade |
		+-----------+-------------+-------+
		| CLERK     | 1037.500000 |     1 |
		| SALESMAN  | 1400.000000 |     2 |
		| ANALYST   | 3000.000000 |     4 |
		| MANAGER   | 2758.333333 |     4 |
		| PRESIDENT | 5000.000000 |     5 |
		+-----------+-------------+-------+

3.5、select后面出现的子查询（这个内容不需要掌握，了解即可！！！）

案例：找出每个员工的部门名称，要求显示员工名，部门名？

	select 
		e.ename,e.deptno,(select d.dname from dept d where e.deptno = d.deptno) as dname 
	from 
		emp e;


	+--------+--------+------------+
	| ename  | deptno | dname      |
	+--------+--------+------------+
	| SMITH  |     20 | RESEARCH   |
	| ALLEN  |     30 | SALES      |
	| WARD   |     30 | SALES      |
	| JONES  |     20 | RESEARCH   |
	| MARTIN |     30 | SALES      |
	| BLAKE  |     30 | SALES      |
	| CLARK  |     10 | ACCOUNTING |
	| SCOTT  |     20 | RESEARCH   |
	| KING   |     10 | ACCOUNTING |
	| TURNER |     30 | SALES      |
	| ADAMS  |     20 | RESEARCH   |
	| JAMES  |     30 | SALES      |
	| FORD   |     20 | RESEARCH   |
	| MILLER |     10 | ACCOUNTING |
	+--------+--------+------------+

	//错误：ERROR 1242 (21000): Subquery returns more than 1 row
	select 
		e.ename,e.deptno,(select dname from dept) as dname
	from
		emp e;
	
	注意：对于select后面的子查询来说，这个子查询只能一次返回1条结果，
	多于1条，就报错了。！




# 15 union合并查询结果集

案例：查询工作岗位是MANAGER和SALESMAN的员工？
	select ename,job from emp where job = 'MANAGER' or job = 'SALESMAN';
	select ename,job from emp where job in('MANAGER','SALESMAN');
	+--------+----------+
	| ename  | job      |
	+--------+----------+
	| ALLEN  | SALESMAN |
	| WARD   | SALESMAN |
	| JONES  | MANAGER  |
	| MARTIN | SALESMAN |
	| BLAKE  | MANAGER  |
	| CLARK  | MANAGER  |
	| TURNER | SALESMAN |
	+--------+----------+
	
	select ename,job from emp where job = 'MANAGER'
	union
	select ename,job from emp where job = 'SALESMAN';
	
	+--------+----------+
	| ename  | job      |
	+--------+----------+
	| JONES  | MANAGER  |
	| BLAKE  | MANAGER  |
	| CLARK  | MANAGER  |
	| ALLEN  | SALESMAN |
	| WARD   | SALESMAN |
	| MARTIN | SALESMAN |
	| TURNER | SALESMAN |
	+--------+----------+

	union的效率要高一些。对于表连接来说，每连接一次新表，
	则匹配的次数满足笛卡尔积，成倍的翻。。。
	但是union可以减少匹配的次数。在减少匹配次数的情况下，
	还可以完成两个结果集的拼接。

	a 连接 b 连接 c
	a 10条记录
	b 10条记录
	c 10条记录
	匹配次数是：1000

	a 连接 b一个结果：10 * 10 --> 100次
	a 连接 c一个结果：10 * 10 --> 100次
	使用union的话是：100次 + 100次 = 200次。（union把乘法变成了加法运算）

union在使用的时候有注意事项吗？

	//错误的：union在进行结果集合并的时候，要求两个结果集的列数相同。
	select ename,job from emp where job = 'MANAGER'
	union
	select ename from emp where job = 'SALESMAN';

	// MYSQL可以，oracle语法严格 ，不可以，报错。要求：结果集合并时列和列的数据类型也要一致。
	select ename,job from emp where job = 'MANAGER'
	union
	select ename,sal from emp where job = 'SALESMAN';
	+--------+---------+
	| ename  | job     |
	+--------+---------+
	| JONES  | MANAGER |
	| BLAKE  | MANAGER |
	| CLARK  | MANAGER |
	| ALLEN  | 1600    |
	| WARD   | 1250    |
	| MARTIN | 1250    |
	| TURNER | 1500    |
	+--------+---------+

# 16、limit（非常重要）
	
5.1、limit作用：将查询结果集的一部分取出来。通常使用在分页查询当中。
百度默认：一页显示10条记录。
分页的作用是为了提高用户的体验，因为一次全部都查出来，用户体验差。
可以一页一页翻页看。

5.2、limit怎么用呢？

	完整用法：limit startIndex, length
		startIndex是起始下标，length是长度。
		起始下标从0开始。

	缺省用法：limit 5; 这是取前5.

	按照薪资降序，取出排名在前5名的员工？
	select 
		ename,sal
	from
		emp
	order by 
		sal desc
	limit 5; //取前5

	select 
		ename,sal
	from
		emp
	order by 
		sal desc
	limit 0,5;

	+-------+---------+
	| ename | sal     |
	+-------+---------+
	| KING  | 5000.00 |
	| SCOTT | 3000.00 |
	| FORD  | 3000.00 |
	| JONES | 2975.00 |
	| BLAKE | 2850.00 |
	+-------+---------+

5.3、注意：mysql当中limit在order by之后执行！！！！！！

5.4、取出工资排名在[3-5]名的员工？
	select 
		ename,sal
	from
		emp
	order by
		sal desc
	limit
		2, 3;
	
	2表示起始位置从下标2开始，就是第三条记录。
	3表示长度。

	+-------+---------+
	| ename | sal     |
	+-------+---------+
	| FORD  | 3000.00 |
	| JONES | 2975.00 |
	| BLAKE | 2850.00 |
	+-------+---------+

5.5、取出工资排名在[5-9]名的员工？
	select 
		ename,sal
	from
		emp
	order by 
		sal desc
	limit
		4, 5;

	+--------+---------+
	| ename  | sal     |
	+--------+---------+
	| BLAKE  | 2850.00 |
	| CLARK  | 2450.00 |
	| ALLEN  | 1600.00 |
	| TURNER | 1500.00 |
	| MILLER | 1300.00 |
	+--------+---------+

# 17、分页

每页显示3条记录
	第1页：limit 0,3		[0 1 2]
	第2页：limit 3,3		[3 4 5]
	第3页：limit 6,3		[6 7 8]
	第4页：limit 9,3		[9 10 11]

每页显示pageSize条记录
	第pageNo页：limit (pageNo - 1) * pageSize  , pageSize

	public static void main(String[] args){
		// 用户提交过来一个页码，以及每页显示的记录条数
		int pageNo = 5; //第5页
		int pageSize = 10; //每页显示10条

		int startIndex = (pageNo - 1) * pageSize;
		String sql = "select ...limit " + startIndex + ", " + pageSize;
	}

记公式：
	limit (pageNo-1)*pageSize , pageSize



# 18、关于mysql中的数据类型？

		varchar(最长255)
			可变长度的字符串
			比较智能，节省空间。
			会根据实际的数据长度动态分配空间。

			优点：节省空间
			缺点：需要动态分配空间，速度慢。

		char(最长255)
			定长字符串
			不管实际的数据长度是多少。
			分配固定长度的空间去存储数据。
			使用不恰当的时候，可能会导致空间的浪费。

			优点：不需要动态分配空间，速度快。
			缺点：使用不当可能会导致空间的浪费。

			varchar和char我们应该怎么选择？
				性别字段你选什么？因为性别是固定长度的字符串，所以选择char。
				姓名字段你选什么？每一个人的名字长度不同，所以选择varchar。


		int(最长11)
			数字中的整数型。等同于java的int。

		bigint
			数字中的长整型。等同于java中的long。

		float	
			单精度浮点型数据

		double
			双精度浮点型数据

		date
			短日期类型

		datetime
			长日期类型

		clob
			字符大对象
			最多可以存储4G的字符串。
			比如：存储一篇文章，存储一个说明。
			超过255个字符的都要采用CLOB字符大对象来存储。
			Character Large OBject:CLOB


		blob
			二进制大对象
			Binary Large OBject
			专门用来存储图片、声音、视频等流媒体数据。
			往BLOB类型的字段上插入数据的时候，例如插入一个图片、视频等，
			你需要使用IO流才行。

	


# 19、date和datetime两个类型的区别？
	date是短日期：只包括年月日信息。
	datetime是长日期：包括年月日时分秒信息。


# 20 约束约束（非常重要，五颗星*****）

### 什么是约束？
	约束对应的英语单词：constraint
	在创建表的时候，我们可以给表中的字段加上一些约束，来保证这个表中数据的
	完整性、有效性！！！

	约束的作用就是为了保证：表中的数据有效！！

### 约束包括哪些？
	非空约束：not null
	唯一性约束: unique
	主键约束: primary key （简称PK）
	外键约束：foreign key（简称FK）
	检查约束：check（mysql不支持，oracle支持）


### 非空约束：not null

	非空约束not null约束的字段不能为NULL。
	create table t_vip(
		id int,
		name varchar(255) not null  // not null只有列级约束，没有表级约束！
	);

### 唯一性约束: unique

	唯一性约束unique约束的字段不能重复，但是可以为NULL
	新需求：name和email两个字段联合起来具有唯一性！！！！
		create table t_vip(
			id int,
			name varchar(255) unique,  // 约束直接添加到列后面的，叫做列级约束。
			email varchar(255) unique
		);
		这张表这样创建是不符合我以上“新需求”的。
		这样创建表示：name具有唯一性，email具有唯一性。各自唯一。

		以下这样的数据是符合我“新需求”的。
		但如果采用以上方式创建表的话，肯定创建失败，因为'zhangsan'和'zhangsan'重复了。
		insert into t_vip(id,name,email) values(1,'zhangsan','zhangsan@123.com');
		insert into t_vip(id,name,email) values(2,'zhangsan','zhangsan@sina.com');

		怎么创建这样的表，才能符合新需求呢？
			drop table if exists t_vip;
			create table t_vip(
				id int,
				name varchar(255),
				email varchar(255),
				unique(name,email) // 约束没有添加在列的后面，这种约束被称为表级约束。
			);
			
		什么时候使用表级约束呢？
			需要给多个字段联合起来添加某一个约束的时候，需要使用表级约束。

	unique 和not null可以联合吗？
		在mysql当中，如果一个字段同时被not null和unique约束的话，
		该字段自动变成主键字段。（注意：oracle中不一样！）

		insert into t_vip(id,name) values(1,'zhangsan');

		insert into t_vip(id,name) values(2,'zhangsan'); //错误了：name不能重复

		insert into t_vip(id) values(2); //错误了：name不能为NULL。

### 主键约束（primary key，简称PK）非常重要：任何一张表都应该有主键，没有主键，表无效！！

	主键约束的相关术语？
		主键约束：就是一种约束。
		主键字段：该字段上添加了主键约束，这样的字段叫做：主键字段
		主键值：主键字段中的每一个值都叫做：主键值。
	
	什么是主键？有啥用？
		主键值是每一行记录的唯一标识。
		主键值是每一行记录的身份证号！！！
	
	特征：
         not null + unique（主键值不能是NULL，同时也不能重复！）

	怎么给一张表添加主键约束呢？
		1个字段做主键，叫做：单一主键
		create table t_vip(
			id int primary key,  //列级约束
			name varchar(255)
		);
	
	id和name联合起来做主键：复合主键！！！！在实际开发中不建议使用：复合主键。建议使用单一主键！因为主键值存在的意义就是这行记录的身份证号，只要意义达到即可，单一主键可以做到。
		复合主键比较复杂，不建议使用！！！
		create table t_vip(
			id int,
			name varchar(255),
			email varchar(255),
			primary key(id,name)
		);
		
	主键除了：单一主键和复合主键之外，还可以这样进行分类？
		自然主键：主键值是一个自然数，和业务没关系。
		业务主键：主键值和业务紧密关联，例如拿银行卡账号做主键值。这就是业务主键！在实际开发中使用业务主键多，还是使用自然主键多一些？自然主键使用比较多，因为主键只要做到不重复就行，不需要有意义。业务主键不好，因为主键一旦和业务挂钩，那么当业务发生变动的时候，可能会影响到主键值，所以业务主键不建议使用。尽量使用自然主键。

	在mysql如何自动维护一个主键值？
		create table t_vip(
			id int primary key auto_increment, //auto_increment表示自增，从1开始，以1递增！
			name varchar(255)
		);
	
		
### 外键约束（foreign key，简称FK）非常重要五颗星*****

	外键约束涉及到的相关术语：
		外键约束：一种约束（foreign key）
		外键字段：该字段上添加了外键约束
		外键值：外键字段当中的每一个值。

  
    测试：外键可以为NULL吗？
		外键值可以为NULL。

	作用：以下例子中。当cno字段没有任何约束的时候，可能会导致数据无效。可能出现一个102，但是102班级不存在。所以为了保证cno字段中的值都是100和101，需要给cno字段添加外键约束。那么：cno字段就是外键字段。cno字段中的每一个值都是外键值。
		请设计数据库表，来描述“班级和学生”的信息？
		第一种方案：班级和学生存储在一张表中？？？
		t_student
		no(pk)			name		classno			classname
		----------------------------------------------------------------------------------
		1					jack			100			北京市大兴区亦庄镇第二中学高三1班
		2					lucy			100			北京市大兴区亦庄镇第二中学高三1班
		3					lilei			100			北京市大兴区亦庄镇第二中学高三1班
		4					hanmeimei	100			北京市大兴区亦庄镇第二中学高三1班
		5					zhangsan		101			北京市大兴区亦庄镇第二中学高三2班
		6					lisi			101			北京市大兴区亦庄镇第二中学高三2班
		7					wangwu		101			北京市大兴区亦庄镇第二中学高三2班
		8					zhaoliu		101			北京市大兴区亦庄镇第二中学高三2班
		分析以上方案的缺点：数据冗余，空间浪费！！！！
		
		
		第二种方案：班级一张表、学生一张表？？
		
		t_class 班级表
		classno(pk)			classname
		------------------------------------------------------
		100					北京市大兴区亦庄镇第二中学高三1班
		101					北京市大兴区亦庄镇第二中学高三1班
	
		t_student 学生表
		no(pk)			name			cno(FK引用t_class这张表的classno)
		----------------------------------------------------------------
		1					jack				100
		2					lucy				100
		3					lilei				100
		4					hanmeimei		100
		5					zhangsan			101
		6					lisi				101
		7					wangwu			101
		8					zhaoliu			101
      


# 21 数据库设计三范式

### 干啥的这是个
    1. 消除冗余，刚开始，人们都是把所有数据放在一个表中，你仔细看这样做的话会有很多数据冗余。比如poject number1对应三个employee，
    任何一个字段变，都是一条新的数据，你就得加一条数据，你为了那区区一个变化的字段，把其他字段都写了一遍，你是傻逼。
    2. 减少依赖。还是好一个例子，你把所有的都放在一起，你这时候project name=lll要改变为cxc，所有相关字段都要改一遍
    这时你数据量如果非常大，累死你。你拆出来一个project ID ，project name表，在别的字段引用的时候只引用peocect id，别的表不用动  
    你只需要改这张表里的procjet name一个字段即可。因为其他表不知道，人家只知道对应你那个projcet id
### 啥时候用的
    拆表的时候。或者说是设计数据库的时候。
### 口诀
    一对多（第三范式）：一对多，两张表，多的表加外键！！！！！！！！！！！！
    多对多（第二范式）：多对多，三张表，关系表两个外键！！！！！！！！！！！！！！！
    一对一（第一范式）：外键唯一！！！！一对一放到一张表中不就行了吗？为啥还要拆分表？  
    原因：在实际的开发中，可能存在一张表字段太多，太庞大。这个时候要拆分表。

### 第一范式：必须有主键，每一个字段原子性不可再分

    最核心，最重要的范式，所有表的设计都需要满足。
	必须有主键，并且每一个字段都是原子性不可再分。

	学生编号 学生姓名 联系方式
	------------------------------------------
	1001		张三		zs@gmail.com,1359999999
	1002		李四		ls@gmail.com,13699999999
	1001		王五		ww@163.net,13488888888

	以上是学生表，满足第一范式吗？
	不满足，第一：没有主键。第二：联系方式可以分为邮箱地址和电话

### 第二范式：无复合主建。建立在第一范式的基础之上，要求所有非主键字段完全依赖主键，不要产生部分依赖。

	学生编号 学生姓名 教师编号 教师姓名
	----------------------------------------------------
	1001			张三		001		王老师
	1002			李四		002		赵老师
	1003			王五		001		王老师
	1001			张三		002		赵老师

	这张表描述了学生和老师的关系：（1个学生可能有多个老师，1个老师有多个学生）
	这是非常典型的：多对多关系！

	分析以上的表是否满足第一范式？
	不满足第一范式。
	
	怎么满足第一范式呢？修改：
	学生编号+教师编号(pk)		学生姓名  教师姓名
	----------------------------------------------------
	1001			001				张三			王老师
	1002			002				李四			赵老师
	1003			001				王五			王老师
	1001			002				张三			赵老师

	学生编号 教师编号，两个字段联合做主键，复合主键（PK: 学生编号+教师编号）
	经过修改之后，以上的表满足了第一范式。但是满足第二范式吗？
		不满足，表格中的一列属性仅有部分主键决定。“张三”依赖1001，“王老师”依赖001，显然产生了部分依赖。产生部分依赖会使数据冗余，空间浪费了。“张三”重复了，“王老师”重复了。
	
	为了让以上的表满足第二范式，你需要这样设计：
		使用三张表来表示多对多的关系！！！！
		学生表
		学生编号(pk)		学生名字
		------------------------------------
		1001					张三
		1002					李四
		1003					王五
		
		教师表
		教师编号(pk)		教师姓名
		--------------------------------------
		001					王老师
		002					赵老师

		学生教师关系表
		id(pk)			学生编号(fk)			教师编号(fk)
		------------------------------------------------------
		1						1001						001
		2						1002						002
		3						1003						001
		4						1001						002
	

	背口诀：
		多对多怎么设计？
			多对多，三张表，关系表两个外键！！！！！！！！！！！！！！！

### 第三范式：建立在第二范式的基础之上，要求所有非主键字段直接依赖主键，不要产生传递依赖。

	学生编号（PK） 学生姓名 班级编号  班级名称
	---------------------------------------------------------
		1001				张三		01			一年一班
		1002				李四		02			一年二班
		1003				王五		03			一年三班
		1004				赵六		03			一年三班
	
	以上表的设计是描述：班级和学生的关系。很显然是1对多关系！
	一个教室中有多个学生。

	分析以上表是否满足第一范式？
		满足第一范式，有主键。
	
	分析以上表是否满足第二范式？
		满足第二范式，因为主键不是复合主键，没有产生部分依赖。主键是单一主键。
	
	分析以上表是否满足第三范式？
		第三范式要求：不要产生传递依赖！
		一年一班依赖01，01依赖1001，产生了传递依赖。
		不符合第三范式的要求。产生了数据的冗余。
	
	那么应该怎么设计一对多呢？

		班级表：一
		班级编号(pk)				班级名称
		----------------------------------------
		01					      一年一班
		02						  一年二班
		03						  一年三班

		学生表：多

		学生编号（PK） 学生姓名 班级编号(fk)
		-------------------------------------------
		1001				张三			01			
		1002				李四			02			
		1003				王五			03			
		1004				赵六			03	

### 嘱咐一句话：

	数据库设计三范式是理论上的。实践和理论有的时候有偏差。最终的目的都是为了满足客户的需求，有的时候会拿冗余换执行速度。

	因为在sql当中，表和表之间连接次数越多，效率越低。（笛卡尔积）有的时候可能会存在冗余，但是为了减少表的连接次数，这样做也是合理的，并且对于开发人员来说，sql语句的编写难度也会降低。

	面试的时候把这句话说上：他就不会认为你是初级程序员了！