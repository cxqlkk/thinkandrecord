
select concat("ALTER TABLE ","`",col.TABLE_NAME,"`"," CHANGE ","`",col.COLUMN_NAME,"`"," ","`",col.COLUMN_NAME,"`"," ",col.COLUMN_TYPE , " ",
if(col.CHARACTER_SET_NAME is null," ",concat(" character set ",col.CHARACTER_SET_NAME," ")),
if(col.COLLATION_NAME is null," ",concat(" COLLATE ","'",col.COLLATION_NAME,"' ")),
if(col.IS_NULLABLE='NO'," NOT NULL "," null "), 
if(col.COLUMN_DEFAULT is null , if(col.EXTRA='auto_increment' or col.IS_NULLABLE='NO'," "," DEFAULT null ") ,concat(" DEFAULT ",if(col.DATA_TYPE='timestamp' or col.DATA_TYPE='bit' ,col.COLUMN_DEFAULT,concat("'",col.COLUMN_DEFAULT,"'")))),
if(col.EXTRA is null ," ",concat(" ",col.EXTRA," "  )),
" COMMENT "," ","'",col.COLUMN_COMMENT,"'",";") change_column_type
from information_schema.COLUMNS col 
join information_schema.tables  tbl  on col.TABLE_SCHEMA=tbl.TABLE_SCHEMA and col.TABLE_NAME=tbl.TABLE_NAME
where col.TABLE_SCHEMA='codenai' and tbl.TABLE_TYPE='BASE TABLE'  ;