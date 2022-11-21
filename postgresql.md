su - postgres
psql
select * from pg_user;
CREATE USER mark_mishenko WITH PASSWORD 'Fb2F7qi9p3bhmj0nBqQ5jlcpjQHdta';
GRANT ALL PRIVILEGES ON DATABASE "database1" to dmosk;
\c database1
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO "dmosk";
GRANT ALL PRIVILEGES ON TABLE table1 IN SCHEMA public TO "dmosk";

\l - вывести список таблиц

GRANT SELECT ON ALL TABLES IN SCHEMA public TO "mark_mishenko";
GRANT SELECT ON ALL TABLES IN SCHEMA public TO "mark_mishenko";

GRANT CONNECT ON DATABASE "rtb" to dmark_mishenko;