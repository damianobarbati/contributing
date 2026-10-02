# Database

Guidelines:
- migration files must never use knex querybuilder, only `database.raw` calls with plain raw sql statements
- migration files must leave `down` handler empty
- all id columns must be defined as `uuidv7`
- all date columns must be defined as `timestamptz(0)`
- all numeric columns must be defined as `numeric`
- all text columns must be defined as `text`, avoid char is not strictly needed
- all enums columns are defined as `<col> text check (col in ('x','y','z'))`
- always put id, created_at, updated_at as first 3 columns of each table
- avoid useless indexes
- apply updated_at trigger to set column to now()