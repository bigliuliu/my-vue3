<template>
    <div class="hello">
      <p>mySql learning is starting</p>
      <div>
       <h3>
         char
       </h3>
       <span>存储指定长度的字符串</span>
       <h3>
         varchar
       </h3>
       <span>存储可变长度的字符串</span>
       <h3>
         limit和offset
       </h3>
       <h4>
        limit : pageSize;
       </h4>
       <h4>
        offset: pageSize*(pageIndex - 1);
       </h4>
       <span>limit : 每页限制多少条数据；offset：当前也的索引</span>
       <h4>
        mySql中：limit 15 offset 30 可以简写为 limit 30，15
       </h4>
       <h3>
        排序
       </h3>
       <span>SELECT id, name, gender, score FROM students WHERE class_id = 1 ORDER BY score DESC;</span>
       <h3>
        聚合查询
       </h3>
       <span>查询student表中共多少条记录：select count(*) from student</span>
       <p>查询student表中男生有多少条记录并将记录命名为boys： select count(*) boys from students where gender = 'F';</p>
       <p>
        sum: 计算一列合计值，该列必须为数值
       </p>
       <p>
        avg：计算某一列的平均值，该列必须为数值
       </p>
       <p>
        max: 计算某一列的最大值
       </p>
       <p>
        min ：计算某一列的最小值
       </p>
       <h3>分组聚合</h3>
       <p>按照class_id分别计算各个班的总数 ：select class_id, count(*) num from students group by class_id</p>
       <p>查询每个班男生和女生的平均值：select class_id, gender, avg(score) from students group by class_id,gender</p>
       <h3>
         内连接（inner join）：
       </h3>
       <span>连接查询两个表，返回的的数据是同时存在与两个表中的记录</span>
       <p>
        SELECT s.id, s.name, s.class_id, c.name class_name, s.gender, s.score FROM students s INNER JOIN classes c ON s.class_id = c.id;
       </p>
       <h3>
         外连接（outer join）：
       </h3>
       <span>分为left outer join ，right join，和full outer join ：连接两个表查询，查询记录结果是存在一个左表或右表中，或者两个表分别都存在数据</span>
       <p>
        SELECT s.id, s.name, s.class_id, c.name class_name, s.gender, s.score FROM students s RIGHT OUTER JOIN classes c ON s.class_id = c.id;
       </p>
       <h3>Insert 插入多条语句：</h3>
       <p>INSERT INTO students (class_id, name, gender, score) VALUES (1, '大宝', 'M', 87), (2, '二宝', 'M', 81);</p>
       <h3>update 更新多条语句：</h3>
       <p>update students set name="哈哈", gender="F" where score = 80;</p>
       <p>update students set score = score +10 where score =50 ;</p>
       <p>update可以省略where ：update student set score = 60</p>
       <h3>delete 删除多条语句：</h3>
       <p>delete from students where id= 10 and score =80;</p>
       <p>删除整个表数据： DELETE FROM students;</p>
       <h3>
        插入或替换
       </h3>
       <p>id=1存在，先删除该记录，在插入新的，不存在则直接插入：</p>
       <span>REPLACE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);</span>
      <h3>插入或更新</h3>
      <p>id = 1存在则更新这条记录，不存在则插入，更新的字段由update指定</p>
      <span>INSERT INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99) ON DUPLICATE KEY UPDATE name='小明', gender='F', score=99;</span>
      <h3>插入或忽略</h3>
      <p>id=1的记录不存在则插入新纪录，否则不执行</p>
      <span>INSERT IGNORE INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'F', 99);</span>
      <h3>快照（复制一份当前表的数据到一个新表）</h3>
      <span> create table copyStudent select * from student where class_id = 1;</span>
      <h3>强制使用指定索引（force index）</h3>
      <span>SELECT * FROM students FORCE INDEX (idx_class_id) WHERE class_id = 1 ORDER BY id DESC;</span>
      <h3>-------------------------数据库事务--------------------------</h3>
      <h3>事务执行</h3>
      <p>
        使用begin开启一个事务，使用commit提交一个事务。这是显示事务
      </p>
      <span>
        BEGIN;
        UPDATE accounts SET balance = balance - 100 WHERE id = 1;
        UPDATE accounts SET balance = balance + 100 WHERE id = 2;
        COMMIT;
      </span>
      <P>commit是提交事务，即试图将事务内所有的sql做的修改永久保存，如果commit语句执行失败，整个事务也会失败。</P>
      <h3>ACID4个特性</h3>
       <p>原子性：将所有的sql作为原子工作单元执行，要么全部执行，要么全部不执行</p>
       <p>一致性：事务完成后，所有数据的状态都是一致性的</p>
       <p>隔离性：多个事务并发执行时，每个事务做出的修改必须与其他事务隔离</p>
       <p>持久性：事务执行完成后，对数据库的修改被持久化存储</p>
       <h3>事务的隔离级别：</h3>
       <p>read uncommitted ：脏读</p>
       <span>一个事务读到了另一个事务更新后但未提交的书库，如果事务回滚，那么当前事务读到的数据就是脏数据。</span>
       <p>在read uncommitted隔离级别下，一个事务读取到另一个事务更新但未提交的数据，这个数据就是脏数据</p>
       <p>read committed ：不可重复读</p>
       <span>在一个事务内，多次读同一个数据，在当前事务还没结束时，另一个事务恰好修改了这个数据，那么在第一个事务中会造成两次读取的数据可能不一致</span>
       <p>在read committed隔离级别下，事务不可以重复读同一条记录，因为很可能读到的结果不一致</p>
       <p>repeatable read: 幻读</p>
       <span>在一个中，第一次查询某条记录，发现没有，但是当试图更新这条不存在的记录时，竟然能成功，并且再次读取同一个记录，它奇迹般的出现了</span>
       <p>幻读就是没有读到的记录以为不存在，但其实时可以更新成功，并且更新成功后，再次读取就出现了</p>
       <p>Serializable</p>
       <span>事务隔离的最高级别，所有事务按照次序依次执行，因为上述情况都不会出现。</span>
       <p>事务具有最高的安全性，但是由于事务是串行执行，所以效率会大大下降，应用程序的性能会极具降低</p>
    </div>
    </div>
  </template>
  
  <script>
  import {defineComponent} from "vue";
  
  export default defineComponent ({
    setup() {

      return {
      };
    },
  })
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>

  </style>
  