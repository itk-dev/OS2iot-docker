# Development

> [!WARNING]
> This document is still work in progress.

Start backend and frontend in development mode (cf. [`docker-compose.development.yml`](docker-compose.development.yml)):

``` shell
task dev:start
task setup:chirpstack
```

Nginx now exposes the frontend on <http://127.0.0.1:8888/> and the backend (API) on <http://127.0.0.1:8888/api/>, e.g.
<http://127.0.0.1:8888/api/v1/docs>.

> [!NOTE]
> You may have to wait quite a while until everything is up and running. And you may have to reload in your browser a
> couple of times …

The frontend is also exposed (bypassing nginx) on <http://0.0.0.0:8081> and the backend on <http://0.0.0.0:3000>.

Check the status development services:

``` shell
task dev:status
curl http://0.0.0.0:8888
curl http://0.0.0.0:8888/api/v1/docs
```

## Frontend

> [!WARNING]
> Incomplete section ahead!

Built with Angular.

## Backend

> [!WARNING]
> Incomplete section ahead!

Built with [Nest (NestJS)](https://docs.nestjs.com/).

``` shell
task dev:log SERVICE=backend
```

### Add new entity

1. Create a new class in `src/entities`, e.g.

   ``` node
   // src/entities/contact-person.entity.ts
   import { DbBaseEntity } from "./base.entity";

   @Entity("contact_person")
   export class ContactPerson extends DbBaseEntity {
     // …
   }
   ```

2. Add the entity to `TypeOrmModule.forFeature` in `src/modules/shared.module.ts`:

   ``` node
   // src/modules/shared.module.ts

   @Module({
     imports: [
       TypeOrmModule.forFeature([
         // …
         ContactPerson,
       ]),
   // …
   ```

3. Generate a migration:

   ``` shell
   docker compose --project-name os2iot-docker exec os2iot-backend npm run generate-migration src/migration/name-of-migration
   ```

### Add entity property (in API)

``` shell

```

---

Talk to the database:

``` shell
docker compose --project-name os2iot-docker exec os2iot-postgresql psql os2iot os2iot
```
