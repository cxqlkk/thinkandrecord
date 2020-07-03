

# 单行
INSERT INTO TABLE (a,b,c)
VALUES (1,2,3) ON DUPLICATE KEY UPDATE c=c+1;


# 多行

insert into Table (a,b,c) values (1,2,3),(1,2,3)
on ON DUPLICATE KEY UPDATE c=values(a),b=values(b) ..