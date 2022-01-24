## 要求二：建立資料庫和資料表
1. 建立一個新的資料庫，取名字為 website。

   ```sql
   CREATE DATABASE `website`;
   ```
2. 在資料庫中，建立會員資料表，取名字為 member。

   ```sql
   CREATE TABLE `member`(
       `id` BIGINT PRIMARY KEY AUTO_INCREMENT, 
       `name` VARCHAR(255) NOT NULL, 
       `username` VARCHAR(255) NOT NULL, 
       `password` VARCHAR(255) NOT NULL, 
       `follower_count` INT NOT NULL DEFAULT '0', 
       `time` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP 
   );
   ```
## 要求三：SQL CRUD
1. 使用 INSERT 指令新增一筆資料到 member 資料表中，這筆資料的 username 和 password 欄位必須是 test。接著繼續新增至少 4 筆隨意的資料。

   ```sql
   INSERT INTO `member`(name,username,password,follower_count) VALUES('小紅','test','test',3);
   INSERT INTO `member`(name,username,password,follower_count) VALUES('小澄','orange','orange',10);
   INSERT INTO `member`(name,username,password,follower_count) VALUES('小黃','yellow','yellow',7);
   INSERT INTO `member`(name,username,password,follower_count) VALUES('小綠','green','green',1);
   INSERT INTO `member`(name,username,password,follower_count) VALUES('小藍','blue','blue',6);
   INSERT INTO `member`(name,username,password,follower_count) VALUES('小紫','purple','purple',12);
   ```
2. 使用 SELECT 指令取得所有在 member 資料表中的會員資料。

   ```sql
   SELECT * FROM `member`;
   ```
3. 使用 SELECT 指令取得所有在 member 資料表中的會員資料，並按照 time 欄位，由近到遠排序。

   ```sql
   SELECT * FROM `member` ORDER BY `time` DESC;
   ```
4. 使用 SELECT 指令取得 member 資料表中第 2 ~ 4 共三筆資料，並按照 time 欄位，由近到遠排序。( 並非編號 2、3、4 的資料，而是排序後的第 2 ~ 4 筆資料 )

   ```sql
   SELECT * FROM `member` ORDER BY `time` DESC LIMIT 1,3;
   ```
5. 使用 SELECT 指令取得欄位 username 是 test 的會員資料。

   ```sql
   SELECT * FROM `member` WHERE `username`='test';
   ```
6. 使用 SELECT 指令取得欄位 username 是 test、且欄位 password 也是 test 的資料。

   ```sql
   SELECT * FROM `member` WHERE `username`='test' and `password`='test';
   ```
7. 使用 UPDATE 指令更新欄位 username 是 test 的會員資料，將資料中的 name 欄位改成 test2。

   ```sql
   UPDATE `member` SET `username`='test2' WHERE `username`='test';
   ```
## 要求四：SQL Aggregate Functions
1. 取得 member 資料表中，總共有幾筆資料 ( 幾位會員 )。

   ```sql
   SELECT COUNT(*) FROM `member`;
   ```
2. 取得 member 資料表中，所有會員 follower_count 欄位的總和。

   ```sql
   SELECT SUM(`follower_count`) FROM `member`;
   ```
3. 取得 member 資料表中，所有會員 follower_count 欄位的平均數。

   ```sql
   SELECT AVG(`follower_count`) FROM `member`;
   ```
## 要求五：SQL JOIN (Optional)
1. 在資料庫中，建立新資料表，取名字為 message。
   
   ```sql
   CREATE TABLE `message`(
      `id` BIGINT PRIMARY KEY AUTO_INCREMENT,
      `member_id` BIGINT NOT NULL,
      `content` VARCHAR(255) NOT NULL,
      `time` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
      FOREIGN KEY (`member_id`) REFERENCES `member`(`id`) ON DELETE CASCADE
   );
   ```
2. 使用 SELECT 搭配 JOIN 語法，取得所有留言，結果須包含留言者會員的姓名。

   ```sql
   SELECT `member`.`name`,`message`.`content`
   FROM `member` JOIN `message`
   ON `member`. `id` = `message`.`member_id`;
   ```
3. 使用 SELECT 搭配 JOIN 語法，取得 member 資料表中欄位 username 是 test 的所有留言，資料中須包含留言者會員的姓名。

   ```sql
   SELECT `member`.`name`,`message`.`content`
   FROM `member` JOIN `message`
   ON `member`. `id` = `message`.`member_id`
   WHERE `username` = 'test';
   ```




