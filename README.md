# Assignment5

要求三：
- 使用 INSERT 指令新增一筆資料到 user 資料表中，這筆資料的 username 和 password 欄位必須是 ply。接著繼續新增至少 4 筆隨意的資料。

 # create user table
 CREATE TABLE user(id BIGINT PRIMARY KEY AUTO_INCREMENT,
 name VARCHAR(255) NOT NULL,
 username VARCHAR(255) NOT NULL,
 password VARCHAR(255) NOT NULL,
 time DATETIME DEFAULT CURRENT_TIMESTAMP);
 
 INSERT INTO user(name, username, password) VALUES('Taehyung', 'ply', 'ply'),
 ('Wheein', 'wh', 'in'),
 ('Jacky', 'jk', 'ad'),
 ('Adria', 'ad', 'jk'),
 ('Tiffany', 'tf', 'ay');
 
 - 使用 SELECT 指令取得所有在 user 資料表中的使用者資料。
 SELECT * FROM user;

- 使用 SELECT 指令取得 user 資料表中總共有幾筆資料。
SELECT COUNT(*) FROM user;

- 使用 SELECT 指令取得所有在 user 資料表中的使用者資料，並按照 time 欄位，由近到遠排序。
SELECT * FROM user ORDER BY time ASC;

- 使用 SELECT 指令取得 user 資料表中第 2 ~ 4 共三筆資料，並按照 time 欄位，由近到遠排序。
SELECT * FROM user WHERE id BETWEEN 2 and 4 ORDER BY time ASC;

- 使用 SELECT 指令取得欄位 username 是 ply 的使用者資料。
SELECT * FROM user WHERE username = 'ply';

- 使用 SELECT 指令取得欄位 username 是 ply、且欄位 password 也是 ply 的資料。
SELECT * FROM user WHERE username = 'ply' AND password = 'ply';

- 使用 UPDATE 指令更新欄位 username 是 ply 的使用者資料，將資料中的 name 欄位改成【丁滿】。
UPDATE user SET name = '丁滿' WHERE username = 'ply';

- 使用 DELETE 指令刪除所有在 user 資料表中的資料。
DELETE FROM user;

要求四：
# create message table
CREATE TABLE message(id BIGINT PRIMARY KEY AUOT_INCREMENT,
user_id BIGINT NOT NULL,
content VARCHAR(255) NOT NULL,
time DATETIME DEFAULT CURRENT_TIMESTAMP,
FOREIGN KEY(user_id) REFERENCES user(id);

# 修改 foregin key 對應
ALTER TABLE user ADD FOREIGN key(id) REFERENCES message(user_id);

- 使用 SELECT 搭配 JOIN 的語法，取得所有留言，資料中須包含留言會員的姓名。
SELECT user.id, user.name, message.content FROM user JOIN message on user.id = message.user_id;

- 使用 SELECT 搭配 JOIN 的語法，取得 user 資料表中欄位 username 是 ply 的所有留言，資料中須包含留言會員的姓名。
SELECT user.id, user.name, user.username, message.content FROM user JOIN message on user.id = message.user_id WHERE user.username = 'ply';
