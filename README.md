# databricks-sqlmigration

CREATE TABLE products_master (
  product_id          INT PRIMARY KEY NOT NULL, -- Added PRIMARY KEY for unique identifier
  product_name        NVARCHAR(255),            -- Use NVARCHAR for Unicode support
  category            NVARCHAR(100),
  price               DECIMAL(10, 2),
  stock_quantity      INT,
  last_updated        DATETIME2                 -- DATETIME2 for precision
);
GO
INSERT INTO products_master (product_id, product_name, category, price, stock_quantity, last_updated) VALUES
(1, 'Laptop Pro', 'Electronics', 1200.00, 50, GETDATE()),
(2, 'Wireless Mouse', 'Electronics', 25.50, 200, GETDATE()),
(3, 'Novel: The Great Adventure', 'Books', 15.99, 150, SYSDATETIME()); -- SYSDATETIME() for higher precision
GO

SELECT * FROM products_master;
![image](https://github.com/user-attachments/assets/ebcfb8e0-1bf9-4c41-abe1-1dc4c9b09207)


Store procedure in SQL Server

-- Ensure you are in the correct database (e.g., your_database_name)
-- USE your_database_name;
-- GO

CREATE PROCEDURE dbo.GetProductNameById
    @ProductId INT -- Input parameter for product_id
AS
BEGIN
    -- Select the product_name from the products_master table
    SELECT product_name
    FROM dbo.products_master -- Make sure to use the correct schema, e.g., dbo or products
    WHERE product_id = @ProductId;
END;
GO


EXEC dbo.GetProductNameById @ProductId = 1;
GO


![image](https://github.com/user-attachments/assets/d737136f-c4e9-4e2e-a375-405cb20c5935)



Databricks SQL

![image](https://github.com/user-attachments/assets/7be39839-e220-46be-9c98-76c686118008)



-- Ensure you're in the correct catalog and schema context where you want to create the function.
-- Let's assume your products_master table is in 'main.products'
USE CATALOG main;
USE SCHEMA products; -- This schema will also be where the function is created

CREATE FUNCTION get_product_name_by_id(product_id_param INT)
RETURNS STRING -- The data type of the value returned (product_name is STRING)
COMMENT 'Returns the product name for a given product ID from products_master table.'
RETURN (
  SELECT MAX(product_name)
  FROM products_master -- References products_master in the current schema (main.products)
  WHERE product_id = product_id_param
);

![image](https://github.com/user-attachments/assets/d5391e79-7950-4e74-8422-75d8991cdaf0)  

![image](https://github.com/user-attachments/assets/83aa1363-f023-453e-aeac-68f998f918bf)



in Spark notebook with spark sql


![image](https://github.com/user-attachments/assets/bc5c5d9d-7aa7-44de-8337-0bd6a6e7be27)  

![image](https://github.com/user-attachments/assets/e1fb24d3-f0e3-4cba-8ae7-dec89aff38fd)

![image](https://github.com/user-attachments/assets/92f7ea4c-1ed3-4184-8296-1699f21bf65b) ..

![image](https://github.com/user-attachments/assets/0d2b3cc1-8934-4a86-9b21-fbe84b71e327)





