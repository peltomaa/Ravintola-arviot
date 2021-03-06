# Ravintola-arviot
## Ominaisuudet
### Näkymät
- Julkinen käyttöliittymä
  - Ravintola kartta
    - Käyttäjä voi etsiä ravintoloita sijainnin, nimen ja kategorioiden perusteella
  - Ravintola näkymä
    - Käyttäjä voi lisätä ravintolalle arvion
- Admin käyttöliittymä
  - Lisää ravintola
  - Muokkaa ravintolaa

### UI
#### Ravintola kartta
![Ravintola kartta](https://github.com/peltomaa/Ravintola-arviot/raw/main/img/map.png "Ravintola kartta")

#### Ravintola näkymä
![Ravintola näkymä](https://github.com/peltomaa/Ravintola-arviot/raw/main/img/item.png "Ravintola näkymä")

#### Ravintola näkymä
![Ravintola näkymä](https://github.com/peltomaa/Ravintola-arviot/raw/main/img/item.png "Ravintola näkymä")

### Kirjaudu/registeröidy
![Kirjaudu tai registeröidy](https://github.com/peltomaa/Ravintola-arviot/raw/main/img/login.png "Kirjaudu tai registeröidy")

### Lisää ravintola
![Lisää ravintola](https://github.com/peltomaa/Ravintola-arviot/raw/main/img/add.png "Lisää ravintola")

### Muokkaa ravintolaa
![Muokkaa ravintolaa](https://github.com/peltomaa/Ravintola-arviot/raw/main/img/edit.png "Muokkaa ravintolaa")


## Tietokanta
![Tietokanta](https://github.com/peltomaa/Ravintola-arviot/raw/main/img/db.png "Tietokanta")

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
  "address" varchar,
  "website" varchar,
  "phone" varchar,
  "lat" bigint,
  "lng" bigint,
  "created_at" timestamp,
  "updated_at" timestamp
);

CREATE TABLE "reviews" (
  "text" varchar,
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
  "created_at" timestamp,
  "updated_at" timestamp
);

ALTER TABLE "resturaunts" ADD FOREIGN KEY ("id") REFERENCES "reviews" ("resturaunt_id");

ALTER TABLE "users" ADD FOREIGN KEY ("id") REFERENCES "reviews" ("user_id");

ALTER TABLE "resturaunts" ADD FOREIGN KEY ("id") REFERENCES "resturaunt_labels" ("resturaunt_id");

ALTER TABLE "labels" ADD FOREIGN KEY ("id") REFERENCES "resturaunt_labels" ("labels_id");

COMMENT ON COLUMN "reviews"."score" IS 'Between 1-5';
```