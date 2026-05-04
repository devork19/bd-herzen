# Лабораторная работа 2

##	Задание 1
[![1zadanie-sql2.png](https://i.postimg.cc/L5NDGJVv/1zadanie-sql2.png)

Export SQL script - https://gist.github.com/devork19/3bb9cc18385021eac2760dcdfdb351f1

```SQL
-- -----------------------------------------------------
-- Table `FirstModel`.`invoice`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `FirstModel`.`invoice` (
  `idinvoice` INT NOT NULL AUTO_INCREMENT,
  `userid` INT NOT NULL,
  `productid` INT NOT NULL,
  `cost` DECIMAL(10,2) NOT NULL,
  PRIMARY KEY (`idinvoice`),
  INDEX `user_idx` (`userid` ASC) VISIBLE,
  INDEX `product_idx` (`productid` ASC) VISIBLE,
  CONSTRAINT `user`
    FOREIGN KEY (`userid`)
    REFERENCES `FirstModel`.`user` (`id`),
  CONSTRAINT `prod`
    FOREIGN KEY (`productid`)
    REFERENCES `FirstModel`.`product` (`idproduct`));
```

##	Задание 2
[![2zadanie-sql2.png](https://i.postimg.cc/ZYHSxZdj/2zadanie-sql2.png)

Export SQL script - https://gist.github.com/devork19/f8ed1fba8159689addfcb4c1859f8f81

```SQL
CREATE TABLE IF NOT EXISTS `mydb`.`Orders` (
    `id` INT NOT NULL AUTO_INCREMENT,
    `shop_id` INT NOT NULL,
    `product_id` INT NOT NULL,
    `fio` VARCHAR(255) NOT NULL,
    `date` DATE NULL,
    `quantity` TINYINT NULL,
    `tel` VARCHAR(255) NULL,
    `confirm` TINYINT NULL,
    PRIMARY KEY (`id`, `shop_id`, `product_id`, `fio`),
    INDEX `fk_shop_order_idx` (`shop_id`),
    INDEX `fk_product_order_idx` (`shop_id`, `product_id`),
    CONSTRAINT `fk_orders_shops`
        FOREIGN KEY (`shop_id`)
        REFERENCES `mydb`.`Shops` (`id`)
        ON DELETE CASCADE ON UPDATE CASCADE,
    CONSTRAINT `fk_orders_products`
        FOREIGN KEY (`shop_id`, `product_id`)
        REFERENCES `mydb`.`Products` (`shop_id`, `id`)
        ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE = InnoDB;
```

## Задание 3
[![image.png](https://i.postimg.cc/SxDdgTrx/image.png)

## Задание 4
- **Целостность БД**: СУБД автоматически отследит связи.   
- **Цепная реакция**: Поскольку для всех связей был установлен параметр `ON DELETE CASCADE`, вместе с магазином исчезнут:
    1. Все товары, привязанные к этому магазину в таблице `Products`.
    2. Все заказы на эти товары в таблице `Orders`.
    3. Все записи о доставках этих заказов в таблице `Deliveries`.
	
## Информация о студенте
Стажков Данила Александрович, 2 курс, ИВТ-2.1