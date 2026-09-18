# Database

Guidelines:
- migration files must never use knex querybuilder, only `database.raw` calls with plain raw sql statements
- migration files must leave `down` handler empty