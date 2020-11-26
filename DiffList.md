# SQL
I use MSSQL as my main language.
The following contents are the differences compared to MSSQL.

### Commands
| Description | MSSQL | MySQL |
| ----------- | ----- | ----- |
| To comment one line | -- | # |

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
@value = N'CThe time that this record be created',
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