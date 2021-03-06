```mysql
CREATE TABLE book(
  id INT UNSIGNED NOT NULL AUTO_INCREMENT,
  name VARCHAR(100) NOT NULL,
  main_category VARCHAR(100) NOT NULL,
  sub_category VARCHAR(100) NOT NULL,
  publisher VARCHAR(100) NOT NULL,
  publication_date DATETIME,
  update_date DATETIME,
  summary VARCHAR(255),
  quantity INT UNSIGNED NOT NULL,
  PRIMARY KEY(id)
);

CREATE TABLE book_detail(
  id INT UNSIGNED NOT NULL AUTO_INCREMENT,
  book_id INT UNSIGNED NOT NULL,
  remaining_status INT UNSIGNED NOT NULL,
  rent_count INT UNSIGNED DEFAULT 0,
  reservation_member_id INT UNSIGNED NOT NULL,
  PRIMARY KEY(id)
);

CREATE TABLE review(
  id INT UNSIGNED NOT NULL AUTO_INCREMENT,
  book_id INT UNSIGNED NOT NULL,
  member_id INT UNSIGNED NOT NULL,
  group_id INT UNSIGNED NOT NULL,
  group_order INT UNSIGNED DEFAULT 0,
  depth INT UNSIGNED DEFAULT 0,
  contents TEXT NOT NULL,
  register_date DATETIME DEFAULT now(),
  update_date DATETIME DEFAULT now(),
  PRIMARY KEY(id)
);

CREATE TABLE book_image(
  id INT UNSIGNED NOT NULL AUTO_INCREMENT,
  book_id INT UNSIGNED NOT NULL,
  origin_name VARCHAR(255) NOT NULL,
  saved_name VARCHAR(255) NOT NULL,
  type VARCHAR(100) NOT NULL,
  size INT UNSIGNED NOT NULL,
  path VARCHAR(255) NOT NULL,
  register_date DATETIME DEFAULT now(),
  PRIMARY KEY(id)
);

CREATE TABLE member(
  id INT UNSIGNED NOT NULL AUTO_INCREMENT,
  github_id VARCHAR(100) NOT NULL,
  name VARCHAR(100) NOT NULL,
  available_book_limit INT DEFAULT 3,
  penalty_date DATETIME,
  PRIMARY KEY(id)
);

CREATE TABLE member_image(
  id INT UNSIGNED NOT NULL AUTO_INCREMENT,
  member_id INT UNSIGNED NOT NULL,
  origin_name VARCHAR(255) NOT NULL,
  saved_name VARCHAR(255) NOT NULL,
  type VARCHAR(100) NOT NULL,
  size INT UNSIGNED NOT NULL,
  path VARCHAR(255) NOT NULL,
  register_date DATETIME DEFAULT now(),
  PRIMARY KEY(id)
);

CREATE TABLE checkout(
  id INT UNSIGNED NOT NULL AUTO_INCREMENT,
  member_id INT UNSIGNED NOT NULL,
  book_id INT UNSIGNED NOT NULL,
  borrow_date DATETIME DEFAULT now(),
  PRIMARY KEY(id)
);

ALTER TABLE book_detail ADD FOREIGN KEY (book_id) REFERENCES book(id);
ALTER TABLE review ADD FOREIGN KEY (book_id) REFERENCES book(id);
ALTER TABLE review ADD FOREIGN KEY (member_id) REFERENCES member(id);
ALTER TABLE book_image ADD FOREIGN KEY (book_id) REFERENCES book(id);
ALTER TABLE member_image ADD FOREIGN KEY (member_id) REFERENCES member(id);
ALTER TABLE checkout ADD FOREIGN KEY (member_id) REFERENCES member(id);
ALTER TABLE checkout ADD FOREIGN KEY (book_id) REFERENCES book(id);

SET FOREIGN_KEY_CHECKS = 0;
DROP TABLE IF EXISTS member;
DROP TABLE IF EXISTS member_image;
DROP TABLE IF EXISTS checkout;
DROP TABLE IF EXISTS book;
DROP TABLE IF EXISTS book_image;
DROP TABLE IF EXISTS book_drop;
DROP TABLE IF EXISTS book_detail;
DROP TABLE IF EXISTS review;
SET FOREIGN_KEY_CHECKS = 1;

```
