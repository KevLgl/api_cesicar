# CesiCar - Api/BackOffice
This documentation helps you start CESICAR Api and BackOffice project. Follow thoses steps to set it ready to use in a local enrironment.
It also provides a great help il focusin on api helpers and understanding of datas.

## ENVIRONMENT
| Language | version     | Description                |
| :-------- | :------- | :------------------------- |
| `php` | `8.1.18` | **Required**. 8.1 minimum |
| `node` | `18.15.0` |  |
| `npm` | `9.5.0` |  |
| `MariaDB` | `15.1` | |

## 1/ install vendors
```bash
  composer install
```
## 2/ install nodes
```bash
npm install
```

## 3/ Create the Database
```bash
php bin/console doctrine:database:create
```

### Check DB columns modifications
```bash
php bin/console doctrine:s:u --dump-sql
```

## 4/ Apply DB columns mdoifciations :
```bash
php bin/console doctrine:s:u --force
```

## Optional/ Create first admin user
in database, add first row in user :
- first_name
- last_name
- gender -> homme or femme or autre
- email -> for login
- password -> hashed with delow php command
- roles -> ["ROLE_ADMIN"]
- driver -> 0 or 1
- is_verified -> 0 or 1
- created_at and updated_at -> set now value
## Optional/Hash your first password
```bash
php bin/console security:hash-password
```
## 5 Start API / BackOffice
```bash
symfony server:start
```
## 6 Run fixtures to furnish the databases with starting datas
```bash
php bin/console doctrine:fixtures:load
```

## Project Helpers
<details>
<summary>Routes</summary>

# ROUTES

## Access BackOffice
127.0.0.1:8000/admin

connect with your credentials or this admin :
  login : florent.gallou@viacesi.fr
  password : password

## Access api
127.0.0.1:8000/api
-> help : https://symfonycasts.com/screencast/api-platform/json-ld

## Access api using helper
127.0.0.1:8000/_profiler
-> help : https://symfonycasts.com/screencast/api-platform/profiler

### Api get all Travels
127.0.0.1:8000/api/travels
```bash

[
  {
    "id": 0,
    "toCesi": true,
    "position": [
      "string"
    ],
    "departure_date": "2023-04-27T23:00:09.018Z",
    "user": {
      "name": "string"
    }
  }
]
```
- toCesi (boulean) :
  - true = travel TO CESI
  - false = travel FROM CESI

- position (json array [number, number]) :
  - if toCesi = true -> position = position from where you start to go to CESI
  - if toCesi = false -> position = position where you go when leaving CESI

- departure_date = datetime from when travel starts
  - to know travel length, calculate time with Km between CESI and position

- user.name = first_name.' '.last_name (of driver)

</details>

<details>
<summary>API LOGIN</summary>

## API LOGIN
127.0.0.1/login -> method post
help -> https://symfonycasts.com/screencast/api-platform-security/data-page-load#play


</details>