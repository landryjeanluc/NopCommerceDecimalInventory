# NopCommerceDecimalInventory
NopCommerce with decimal Inventory management (NOP 3.90)

DECLARE @Table as nvarchar(max) , @Column as nvarchar(max)
DECLARE tablecursor Cursor for
  SELECT  Table_Name, Column_Name
  FROM [DATABASE].INFORMATION_SCHEMA.COLUMNS
  Where COLUMN_NAME in ('Quantity','StockQuantity')
OPEN tablecursor
FETCH NEXT FROM tablecursor INTO @Table, @Column
WHILE @@FETCH_STATUS = 0
BEGIN
  EXEC('alter table ['+ @Table +'] alter column ['+ @Column +'] Decimal(18,3) not null')
  FETCH NEXT FROM tablecursor INTO @Table, @Column
END
CLOSE tablecursor
DEALLOCATE tablecursor