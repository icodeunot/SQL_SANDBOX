**Schema (MySQL v5.7)**

    /* CREATING TABLES FROM JAUNTY COFFEE CO. ERD */
    
    CREATE TABLE EMPLOYEE (
      employee_id INT,
      first_name VARCHAR(30),
      last_name VARCHAR(30),
      hire_date DATE,
      job_title VARCHAR(30),
      shop_id INT,
      PRIMARY KEY (employee_id)
    );
    
    CREATE TABLE COFFEE_SHOP (
      shop_id INT,
      shop_name VARCHAR(50),
      city VARCHAR(50),
      state CHAR(2),
      PRIMARY KEY (shop_id)
    );
    
    ALTER TABLE EMPLOYEE    /* ADDING FOREIGN KEY TO EMPLOYEE TABLE, FROM COFFEE_SHOP TABLE PRIMARY KEY AFTER COFFEE_SHOP TABLE CREATION */
    ADD FOREIGN KEY (shop_id) REFERENCES COFFEE_SHOP (shop_id);
    
    CREATE TABLE COFFEE (
      coffee_id INT,
      shop_id INT,
      supplier_id INT,
      coffee_name VARCHAR(30),
      price_per_pound NUMERIC(5,2),
      PRIMARY KEY (coffee_id),
      FOREIGN KEY (shop_id) REFERENCES COFFEE_SHOP(shop_id)
    );
    
    CREATE TABLE SUPPLIER (
      supplier_id INT,
      company_name VARCHAR(50),
      country VARCHAR(30),
      sales_contact_name VARCHAR(60),
      email VARCHAR(50) NOT NULL,
      PRIMARY KEY (supplier_id)
    );
    
    ALTER TABLE COFFEE   /* ADDING FOREIGN KEY TO COFFEE TABLE, FROM SUPPLIER TABLE PRIMARY KEY AFTER SUPPLIER TABLE CREATION */
    ADD FOREIGN KEY (supplier_id) REFERENCES SUPPLIER (supplier_id);
    
    /* INSERTING MY VALUES INTO THE TABLES */
    
    INSERT INTO COFFEE_SHOP (shop_id, shop_name, city, state)
    VALUES (1, 'Javant One?', 'San Diego', 'CA'),
           (2, 'Brew 4 You', 'Midvale', 'UT'),
    	   (3, 'Cafe Eine', 'Santa Fe', 'NM');
           
    INSERT INTO SUPPLIER (supplier_id, company_name, country, sales_contact_name, email)
    VALUES (1, 'Bean Bros', 'Brazil', 'Bobby', 'bobby@beanbros.com'),
    	   (2, 'Wholebean Wholesale', 'Wales', 'Wanda', 'wanda@beanwholesale.com'),
           (3, 'Jittery Delivery', 'Java', 'Jack', 'javajack@jitdev.com');
    
    INSERT INTO COFFEE (coffee_id, shop_id, supplier_id, coffee_name, price_per_pound)
    VALUES (1, 1, 1, 'Single Roast Blonde', 9.99),
    	   (2, 2, 2, 'Twice Roasted Medium', 10.10),
           (3, 3, 3, 'Tri-State Dark', 11.12);
           
    INSERT INTO EMPLOYEE (employee_id, first_name, Last_name, hire_date, job_title, shop_id)
    VALUES (1, 'Javantae', 'Jackson', '20211112', 'Jaunty CEO', 1),
    	   (2, 'Brissa', 'Bolsenaro', '20220506', 'Boardmember', 2),
    	   (3, 'Carly', 'Cantor', '20220605', 'Cashier', 3);
    
    /* VIEW CREATION - PART B SECTION 3 */
    
    CREATE VIEW Employee_View AS
    SELECT 'employee_id', 
    	Concat(EMPLOYEE.first_name,' ',EMPLOYEE.last_name) 
        employee_full_name,
        hire_date,
        job_title,
        shop_id
        FROM EMPLOYEE;
        
    /* INDEX CREATION - PART B SECTION 4 */
    
    CREATE INDEX coffee_name ON COFFEE (coffee_name);