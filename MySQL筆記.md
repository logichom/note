手動更新要加這段

```sql
SET SQL_SAFE_UPDATES = 0;
```

查看版本

```sql
SELECT @@version;
```

查看目前連線數

```sql
show full processlist;
```

最大連線數

```sql
show full processlist;
```

新增table

```sql
CREATE TABLE `test_db`.`attrule` (
  `id` INT(11) NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(30) NULL,
  `wktime` TIME NULL,
  `gtofftime` TIME NULL,
  `smaxtime` INT(11) NULL,
  `tmaxtime` INT(11) NULL,
  `wkovtime` DECIMAL(3,1) NULL,
  `vacation` TINYINT(4) NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8;
```

刪除資料

```sql
Delete from test_db.attresult where ID >0;
```

刪除表

```sql
DROP TABLE IF EXISTS test_db.hr_attresult;
```

更新資料

```sql
UPDATE `test_db`.`viplevel` SET `birthdiscounts`='95' WHERE `levelid`='2';
```

status 欄位依照2、4、1、3順序排序

```sql
select * from corp ORDER BY FIELD(status,'2','4','1','3');
```

SUM+CASE

```sql
SELECT
SUM(CASE WHEN `pay_type`="manual" THEN `amt` ELSE 0 END) AS manual_amt,
SUM(CASE WHEN `pay_type`="electronic" THEN `amt` ELSE 0 END) AS electronic_amt,
SUM(`amt`) AS total_amt
FROM pay
SELECT SUM(case when State=1 then SellingPrice else 0 end),
SUM(case when State=2 then SellingPrice else 0 end),
SUM(case when State=3 then SellingPrice else 0 end);
```

count+if

```sql
SELECT
count(if(State = 1 and urgent = 1,1,null)) as cnt1,
count(if(State = 1 and urgent = 2,1,null)) as cnt2,
count(if(State = 1 and urgent = 3,1,null)) as cnt3,
count(if(State = 1 and urgent = 4,1,null)) as cnt4
FROM test_db.deposit
WHERE 1=1
and CNid>'0' and LocationId = 10 and barcode like '00308401127%';
```

批次更新

```sql
update test_db.goodslist
join test_db.groupd on goodslist.goodsID = groupd.goodsid
set goodsSellprice = 500
where groupid = 22;
```

批次新增

```sql
INSERT INTO test_db.groupd (groupid,goodsid)
select 32,goodsid from marjorie2.groupd
where groupid = 22;
```

更新來自同一張表

```sql
SET SQL_SAFE_UPDATES = 0;
update test_db.trade t1
inner join  apparelshop.trade t2 on
(t1.TId = t2.TId and t2.salespt > (t2.Pick1+t2.Pick2) and t2.State  >1 and t2.salespt <> 0 and t2.ReportDay >= '2017-12-25')
set t1.salespt = t2.Pick1+t2.Pick2;
```

新增不重複

```sql
INSERT INTO test_db.remidata (orderlistID,data0,data1,data2,createTime,checktime,remiMark,RefundAcc,RefundCash)
select $orderid,'','','',now(),now(),1,'',0 from dual
where not exists( select 1 from marjorie2.remidata where orderlistID = $orderid);
```

大量批次更新

```sql
INSERT INTO students
(id, score1, score2)
VALUES
(1, 5, 8),
(2, 10, 8),
(3, 8, 3),
(4, 10, 7)
ON DUPLICATE KEY UPDATE
score1 = VALUES(score1),
score2 = VALUES(score2);
```

檢查設定

```sql
SELECT @@GLOBAL.sql_mode;
-- SELECT @@SESSION.sql_mode;
-- SELECT @@sql_mode;
-- 更改設定 重開機會失效
set sql_mode = '';
set GLOBAL sql_mode = '';
```

暫解資料表亂碼

```sql
set names 'latin1';
```

開啟查詢log

```sql
SHOW VARIABLES LIKE 'general_log';
SET GLOBAL general_log = 'ON';-- 'OFF'
-- 路徑: c:\\wamp64\\bin\\mysql\\mysql5.7.28\\data\\yourcomputername.log
```

join 需要先排序的資料表

> INNER JOIN = JOIN，不過語意更明顯

```sql
SELECT B.user_id, B.ship_no FROM
(
    SELECT `ship_no`,MAX(`insert_time`) insert_time
    FROM log
    WHERE ship_no = 'XXXXXXXX'
    AND type = 'ABC'
    GROUP BY `ship_no`
) A INNER JOIN log B USING (`ship_no`,`insert_time`);
```

BETWEEN 陷阱

例如查詢7/26~8/25資料

```sql
SELECT * FROM order WHERE order_date BETWEEN '2023-07-26' AND '2023-08-25';
```

以上實際查詢的日期區間為2023/7/26 00:00:00~2023/8/25 00:00:00

因為少了時分秒，默認查詢00:00:00，這樣就少一天的資料

以下為建議寫法

```sql
-- 改法1
SELECT * FROM order WHERE order_date BETWEEN '2023-07-26 00:00:00' AND '2023-08-25 23:59:59';
-- 改法2
SELECT * FROM order WHERE order_date BETWEEN '2023-07-26' AND '2023-08-26';
-- 改法3
SELECT * FROM order WHERE order_date >= '2023-07-26 00:00:00' AND order_date <= '2023-08-25 23:59:59';
-- 改法4
SELECT * FROM order WHERE order_date >= '2023-07-26 00:00:00' AND order_date < '2023-08-26 00:00:00';
```
