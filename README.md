# Ravintola-arviot

## Ominaisuudet
### Näkymät
- Julkinen käyttöliittymä
  - Ravintola kartta
    - Käyttäjä voi etsiä ravintoloita sijainnin, nimen ja kategorioiden perusteella
  - Ravintola näkymä
    - Käyttäjä voi lisätä ravintolalle arvion
- Admin käyttöliittymä
  - Ravintola näkymä
    - Lisää ravintola
    - Muokkaa ravintolaa
    - Poista ravintola
### Tietokanta
![Tietokanta](https://github.com/peltomaa/Ravintola-arviot/raw/main/db.png "Tietokanta")
### SQL
```sql
CREATE TYPE "user_roles" AS ENUM (
  'user',
  'admin'
);

CREATE TABLE "users" (
  "id" SERIAL PRIMARY KEY,
  "name" varchar,
  "role" user_roles,
  "created_at" timestamp,
  "updated_at" timestamp
);

CREATE TABLE "resturaunts" (
  "id" SERIAL PRIMARY KEY,
  "name" varchar,
  "lat" bigint,
  "lng" bigint,
  "created_at" timestamp,
  "updated_at" timestamp
);

CREATE TABLE "reviews" (
  "name" varchar,
  "score" int,
  "resturaunt_id" int,
  "user_id" int,
  "created_at" timestamp,
  "updated_at" timestamp
);

CREATE TABLE "resturaunt_labels" (
  "id" SERIAL PRIMARY KEY,
  "resturaunt_id" int,
  "labels_id" int
);

CREATE TABLE "labels" (
  "id" SERIAL PRIMARY KEY,
  "name" varchar,
  "color" varchar,
  "created_at" timestamp,
  "updated_at" timestamp
);

ALTER TABLE "resturaunts" ADD FOREIGN KEY ("id") REFERENCES "reviews" ("resturaunt_id");

ALTER TABLE "users" ADD FOREIGN KEY ("id") REFERENCES "reviews" ("user_id");

ALTER TABLE "resturaunts" ADD FOREIGN KEY ("id") REFERENCES "resturaunt_labels" ("resturaunt_id");

ALTER TABLE "labels" ADD FOREIGN KEY ("id") REFERENCES "resturaunt_labels" ("labels_id");

COMMENT ON COLUMN "reviews"."score" IS 'Between 1-5';
```
