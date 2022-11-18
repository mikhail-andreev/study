su - postgres
psql
select * from pg_user;
CREATE USER dmosk WITH PASSWORD 'myPassword';
GRANT ALL PRIVILEGES ON DATABASE "database1" to dmosk;
\c database1
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO "dmosk";
GRANT ALL PRIVILEGES ON TABLE table1 IN SCHEMA public TO "dmosk";