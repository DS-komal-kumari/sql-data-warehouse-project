USE DataWarehouse;
GO
CREATE OR ALTER PROCEDURE bronze.load_bronze
AS
BEGIN
    DECLARE @start_time DATETIME,
            @end_time DATETIME;

    BEGIN TRY

        PRINT '================================================';
        PRINT 'Loading Bronze Layer';
        PRINT '================================================';

        PRINT '================================================';
        PRINT 'Loading CRM Tables';
        PRINT '================================================';

        SET @start_time = GETDATE();

        PRINT '>> Truncate table: bronze.crm_cust_info';

        TRUNCATE TABLE bronze.crm_cust_info;

        PRINT '>> Insert data into: bronze.crm_cust_info';

        BULK INSERT bronze.crm_cust_info
        FROM 'C:\Users\kg317\Downloads\sql-data-warehouse-project\sql-data-warehouse-project\datasets\source_crm\cust_info.csv'
        WITH (
            FIRSTROW = 2,
            FIELDTERMINATOR = ',',
            TABLOCK
        );

        PRINT '>> Truncate table: bronze.crm_prd_info';

        TRUNCATE TABLE bronze.crm_prd_info;

        BULK INSERT bronze.crm_prd_info
        FROM 'C:\Users\kg317\Downloads\sql-data-warehouse-project\sql-data-warehouse-project\datasets\source_crm\prd_info.csv'
        WITH (
            FIRSTROW = 2,
            FIELDTERMINATOR = ',',
            TABLOCK
        );

        PRINT '>> Truncate table: bronze.crm_sales_details';

        TRUNCATE TABLE bronze.crm_sales_details;

        BULK INSERT bronze.crm_sales_details
        FROM 'C:\Users\kg317\Downloads\sql-data-warehouse-project\sql-data-warehouse-project\datasets\source_crm\sales_details.csv'
        WITH (
            FIRSTROW = 2,
            FIELDTERMINATOR = ',',
            TABLOCK
        );

        PRINT '================================================';
        PRINT 'Loading ERP Tables';
        PRINT '================================================';

        PRINT '>> Truncate table: bronze.erp_loc_a101';

        TRUNCATE TABLE bronze.erp_loc_a101;

        BULK INSERT bronze.erp_loc_a101
        FROM 'C:\Users\kg317\Downloads\sql-data-warehouse-project\sql-data-warehouse-project\datasets\source_erp\loc_a101.csv'
        WITH (
            FIRSTROW = 2,
            FIELDTERMINATOR = ',',
            TABLOCK
        );

        PRINT '>> Truncate table: bronze.erp_px_cat_giv2';

        TRUNCATE TABLE bronze.erp_px_cat_giv2;

        BULK INSERT bronze.erp_px_cat_giv2
        FROM 'C:\Users\kg317\Downloads\sql-data-warehouse-project\sql-data-warehouse-project\datasets\source_erp\PX_CAT_G1V2.csv'
        WITH (
            FIRSTROW = 2,
            FIELDTERMINATOR = ',',
            TABLOCK
        );

        PRINT '>> Truncate table: bronze.erp_cust_az12';

        TRUNCATE TABLE bronze.erp_cust_az12;

        BULK INSERT bronze.erp_cust_az12
        FROM 'C:\Users\kg317\Downloads\sql-data-warehouse-project\sql-data-warehouse-project\datasets\source_erp\cust_az12.csv'
        WITH (
            FIRSTROW = 2,
            FIELDTERMINATOR = ',',
            TABLOCK
        );

        SET @end_time = GETDATE();
        print '> load duration ' +  cast(datediff(second, @start_time, @end_time) as nvarchar) + 'second';
        print '>>--------------------'

        PRINT '================================================';
        PRINT 'Bronze Layer Loaded Successfully';
        PRINT 'Start Time: ' + CAST(@start_time AS VARCHAR(30));
        PRINT 'End Time: ' + CAST(@end_time AS VARCHAR(30));
        PRINT 'Duration (Seconds): '
              + CAST(DATEDIFF(SECOND, @start_time, @end_time) AS VARCHAR(20));
        PRINT '================================================';

    END TRY

    BEGIN CATCH

        PRINT '===================================';
        PRINT 'Error occurred during Bronze Layer loading';
        PRINT 'Error Message: ' + ERROR_MESSAGE();
        PRINT 'Error Number: ' + CAST(ERROR_NUMBER() AS VARCHAR(10));
        PRINT 'Error State: ' + CAST(ERROR_STATE() AS VARCHAR(10));
        PRINT 'Error Line: ' + CAST(ERROR_LINE() AS VARCHAR(10));
        PRINT '===================================';

        THROW;

    END CATCH;

END;
GO

EXEC bronze.load_bronze;
