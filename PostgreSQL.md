CREATE DATABASE call_list;

\c call_list

CREATE TABLE users (
  id SERIAL,
  first_name VARCHAR(15),
  email VARCHAR(30),
  PRIMARY KEY (id)
);

INSERT INTO users (first_name, email) VALUES (
  'Carlos',
  'carlithos@gmail.com'
),
(
  'Laura',
  'laura1998@gmail.com'
);

CREATE TABLE calls (
  id SERIAL,
  phone VARCHAR,
  call_date DATE,
  user_id INTEGER,
  FOREIGN KEY (user_id) REFERENCES users(id)
);

ALTER TABLE users ADD COLUMN last_name VARCHAR(15);

UPDATE users SET last_name = 'Hidalgo' WHERE first_name = 'Carlos';

UPDATE users SET last_name = 'Fajardo' WHERE first_name = 'Laura';

INSERT INTO calls (phone, call_date, user_id) VALUES ('56984975062', '2018-12-17', 2),
  ('56984975062', '2018-03-28', 2), ('56984975062', '2018-03-20', 2),
  ('56984975062', '2018-11-2', 2), ('56984975062', '2018-01-28', 2),
  ('56984975062', '2018-02-27', 2
);

INSERT INTO calls (phone, call_date, user_id) VALUES ('56984975062', '2018-12-17', 1),
  ('56984975062', '2018-03-28', 1), ('56984975062', '2018-03-20', 1),
  ('56984975062', '2018-11-1', 1
);

INSERT INTO users (first_name, last_name, email) VALUES (
  'Ignacio',
  'Olea',
  'nachoolea@gmail.com'
);

SELECT first_name, COUNT(phone) FROM calls FULL JOIN users ON user_id = users.id GROUP BY first_name;

SELECT first_name, phone, call_date FROM calls FULL JOIN users ON user_id = users.id WHERE first_name = 'Carlos' ORDER BY call_date DESC;

CREATE TABLE audits (
  id SERIAL,
  delete_reason VARCHAR(100),
  call_id INTEGER,
  FOREIGN KEY (calls_id) REFERENCES calls(id)
);
