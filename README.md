# UzChess Backend

REST API for **UzChess**, a chess education platform with online courses and lessons with quizzes, a book library, news, a souvenir shop with a cart, player ratings and match history.

Frontend: [uzchess-frontend-nextjs](https://github.com/xayrullayevamuslima34-blip/uzchess-frontend-nextjs)

![NestJS](https://img.shields.io/badge/NestJS-E0234E?logo=nestjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![TypeORM](https://img.shields.io/badge/TypeORM-FE0803)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)

## Highlights

- **60+ controllers** across 9 feature modules, each with separate `public/*` and `admin/*` APIs
- **Auth with OTP verification**, JWT, password hashing with argon2 and role-based guards
- **Courses:** categories, sections, lessons, lesson questions and user answers, progress tracking, reviews, likes and purchases
- **Shop:** souvenirs with colors, images, reviews, likes and a cart
- **Chess:** players and matches
- **Repository layer** on top of TypeORM, with filter DTOs for pagination and search
- **File uploads** with Multer, sorted into folders by file type
- **Env validation** with Joi, so the app fails fast on startup if config is missing
- **Docker Compose** setup for the API and PostgreSQL
- **Swagger** docs

## Project structure

```
src/
  config/          # TypeORM data source, JWT, Multer, Swagger
  core/            # decorators, enums, global exception filter, guards, base repositories
  features/
    authorization/ # register, login, OTP codes
    common/        # users, countries, languages, difficulties, terms
    courses/       # courses, sections, lessons, questions, reviews, purchases
    library/       # books, authors, categories, reviews, likes
    news/          # news and views
    souvenirs/     # souvenirs, colors, images, reviews, likes
    cart/          # cart items
    chess/         # players and matches
    report/        # user reports and report categories
```

Each feature module follows the same layout: `controllers / services / repositories / entities / dtos / filters`.

## Getting started

Requirements: Node.js 20+, PostgreSQL 14+

```bash
npm install
cp .env.example .env   # fill in the values
npm run generate       # first run only: generate the initial migration from entities
npm run migrate        # build and apply migrations
npm run start:dev
```

The API runs at `http://localhost:8008`. Swagger UI is at **http://localhost:8008/docs**.

### With Docker

```bash
cp .env.example .env   # set DB_URL host to "db"
docker compose up --build
```

## API overview

| Prefix | Access | Example |
|---|---|---|
| `/auth` | public | sign-up, sign-in, verify / resend OTP, forgot / reset password |
| `/public/*` | public / user | `GET /public/courses`, `POST /public/cartItems` |
| `/admin/*` | admin (Bearer token) | `POST /admin/courses`, `PATCH /admin/souvenirs/:id` |

See Swagger for the full list of endpoints and request/response schemas.
