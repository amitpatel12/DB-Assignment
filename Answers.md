## 1. Explain the relationship between the "Product" and "Product_Category" entities from the above diagram.

One product can only belong to one category, but a category can have multiple products, according to the one-to-many relationship between the "Product" and "Product_Category" entities. The "Product" table's foreign key category_id, which refers to the "Product_Category" table's primary key id, establishes this relationship. It indicates that every product belongs to a single category, which is specified in the "Product_Category" table.

## 2. How could you ensure that each product in the "Product" table has a valid category assigned to it?

we can use foreign key constraints to enforce referential integrity and make sure that every product in the "Product" table has a valid category assigned to it. This constraint would make sure that the value in the "Product" table's category_id column must also exist in the "Product_Category" table's id column. This guarantees that a product won't be connected to a category that doesn't exist. In order to guarantee that a product cannot be created or updated without providing a valid category, we can also incorporate appropriate validation checks into application logic.

## 3. Create schema in any Database script or any ORM (Object Relational Mapping).
```
CREATE TABLE product (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    desc TEXT,
    SKU VARCHAR(50),
    category_id INT,
    inventory_id INT,
    price DECIMAL(10, 2) NOT NULL,
    discount_id INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    modified_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP,
    FOREIGN KEY (category_id) REFERENCES product_category(id),
    FOREIGN KEY (inventory_id) REFERENCES product_inventory(id),
    FOREIGN KEY (discount_id) REFERENCES discount(id)
);

CREATE TABLE product_category (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    desc TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    modified_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE TABLE product_inventory (
    id INT PRIMARY KEY AUTO_INCREMENT,
    quantity INT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    modified_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE TABLE discount (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    desc TEXT,
    discount_percent DECIMAL(5, 2) NOT NULL,
    active BOOLEAN DEFAULT true,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    modified_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

```
