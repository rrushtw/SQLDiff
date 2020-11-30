# SQL
I use MSSQL as my main language.
<br />
The following contents are the differences compared to MSSQL.

### Commands
| Description | MSSQL | MySQL |
| ----------- | ----- | ----- |
| To comment one line | -- | # or -- |
| To comment a part | /**/ | /**/ |

### SELECT TOP Clause
MSSQL, MS Access
```bash
SELECT TOP 10 MyColumn FROM MyTable ORDER BY CreatedTime;
```
MySQL
```bash
SELECT MyColumn FROM MyTable ORDER BY CreatedTime LIMIT 10;
```
Oracle
```bash
SELECT MyColumn FROM MyTable WHERE ROWNUM < 11 ORDER BY CreatedTime;
```

### IF ELSE Statement
MSSQL
```bash
IF (condition_1)
BEGIN
	SELECT 'condition 1' AS MyResult;
END;
ESLE IF (condition_2)
BEGIN
	SELECT 'condition 2' AS MyResult;
END;
ELSE
BGIN
	SELECT 'else condition' AS MyResult;
END;
```

MySQL, MS Access
```bash
IF (condition_1) THEN
	SELECT 'condition 1' AS MyResult;
ELSEIF (condition_2) THEN
	SELECT 'condition 2' AS MyResult;
ELSE
	SELECT 'else condition' AS MyResult;
END IF;
```

Oracle
```bash
IF (condition_1) THEN
	SELECT 'condition 1' AS MyResult;
ELSIF (condition_2) THEN
	SELECT 'condition 2' AS MyResult;
ELSE
	SELECT 'else condition' AS MyResult;
END IF;
```

### NULL Functions
In order to "SELECT MyColumn FROM MyTable;", and show empty when the value is null

MSSQL
```bash
SELECT ISNULL(MyColumn, '') AS MyNewColumn FROM MyTable WITH(NOLOCK);
```

MySQL
```bash
SELECT IFNULL(MyColumn, '') AS MyNewColumn FROM MyTable;
OR
SELECT COALESCE(MyColumn, '') AS MyNewColumn FROM MyTable;
```

MS Access
```bash
#IsNull in Access is boolean function.
#IFF(boolean, ValueOfTrue, ValueOfFalse)
SELECT IIF(IsNull(MyColumn), 0, MyColumn) AS MyNewColumn FROM MyTable;
```

Oracle
```bash
SELECT NVL(MyColumn, '') AS MyNewColumn FROM MyTable;
```

### Create Table
MSSQL
```bash
CREATE TABLE MyTable (
	Id INT NOT NULL Identity(1, 1),
	MyColumn VARCHAR(10) NULL,
	CreatedTime DATETIME NOT NULL
);
GO

ALTER TABLE MyTable
ADD CONSTRAINT PK_MyTable PRIMARY KEY (Id) WITH(ONLINE = ON) ON [PRIMARY];
GO

CREATE NONCLUSTERED INDEX Index_1
ON MyTable (CreatedTime ASC) WITH(ONLINE = ON) ON [PRIMARY];
GO

EXEC sys.sp_addextendedproperty
@name = N'MS_Description',
@value = N'Comment of MyColumn',
@level0type = N'SCHEMA',
@level0name = N'dbo',
@level1type = N'TABLE',
@level1name = N'MyTable',
@level2type = N'COLUMN',
@level2name = N'MyColumn'
GO

EXEC sys.sp_addextendedproperty
@name = N'MS_Description',
@value = N'The time that this record be created',
@level0type = N'SCHEMA',
@level0name = N'dbo',
@level1type = N'TABLE',
@level1name = N'MyTable',
@level2type = N'COLUMN',
@level2name = N'CreatedTime'
GO

EXEC sys.sp_addextendedproperty
@name=N'MS_Description',
@value=N'My demo table',
@level0type=N'SCHEMA',
@level0name=N'dbo',
@level1type=N'TABLE',
@level1name=N'MyTable'
GO

```

MySQL
```bash
CREATE TABLE MyTable (
	Id INT NOT NULL AUTO_INCREMENT,
	MyColumn VARCHAR(10) NULL COMMENT 'Comment of MyColumn',
	CreateTime DATETIME NOT NULL COMMENT 'The time that this record be created',
	PRIMARY KEY (Id)
);

CREATE INDEX Index_1
ON MyTable (CreateTime);

ALTER TABLE MyTabel
COMMENT = 'My demo table';
```