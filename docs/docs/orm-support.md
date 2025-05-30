# ORM and Query Builder Support

The following ORMs and Query Builders are known to work properly with
PGlite:

## Drizzle

[Drizzle](https://orm.drizzle.team) is a TypeScript ORM with support for many
databases, including PGlite. Features include:

- A declarative relational query API
- An SQL-like query builder API
- Migrations

To use PGlite with Drizzle, wrap you PGlite instance with a `drizzle()` call:

```sh
npm i drizzle-orm @electric-sql/pglite
npm i -D drizzle-kit
```

```ts
import { PGlite } from '@electric-sql/pglite';
import { drizzle } from 'drizzle-orm/pglite';

const client = new PGlite();
const db = drizzle(client);

await db.select().from(...);
```

See the [Drizzle documentation](https://orm.drizzle.team/docs/connect-pglite)
for more details.

## Knex.js

[Knex](https://knexjs.org/) is a stable, reliable Query Builder for various
database engines. Key features include:

- Query builder
- Schema builder
- Raw queries
- Database migration tool

To use Knex.js with PGlite, add knex and the third party [knex-pglite](https://github.com/czeidler/knex-pglite)
library to your project:

```bash
npm i @electric-sql/pglite knex knex-pglite
```

Then you can setup a regular Knex instance:

```javascript
import { knex } from 'knex'
import ClientPgLite from 'knex-pglite'

export const db = knex({
  client: ClientPgLite,
  dialect: 'postgres',
  connection: { connectionString: 'idb://my-database' },
})
```

Now you can check [Knex documentation](https://knexjs.org/guide/query-builder.html)
and [knex-pglite](https://github.com/czeidler/knex-pglite) documentation for
more details.

## TypeORM

[TypeORM](https://typeorm.io/) is an ORM that can run in NodeJS, the Browser, and many other platforms. Key features include:

- Clean object-relational model
- Eager and lazy associations (relations)
- Automatic migration generation
- Elegant-syntax, flexible and powerful QueryBuilder.

To use TypeORM with PGlite, add the third party [typeorm-pglite](https://www.npmjs.com/package/typeorm-pglite)
library to your project:

```bash
npm i @electric-sql/pglite typeorm-pglite
```

typeorm-pglite works with TypeORM's existing postgres dialect. Just provide the PGliteDriver to the driver data source option:

```javascript
import { PGliteDriver, getPGliteInstance } from 'typeorm-pglite'
import { DataSource } from 'typeorm'

const PGliteDataSource = new DataSource({
  type: 'postgres',
  driver: new PGliteDriver().driver,
})

// You can access the internal PGlite instance using getPGliteInstance function
const pgliteDb = await getPGliteInstance()
```

Check [TypeORM documentation](https://typeorm.io/data-source)
and [typeorm-pglite](https://github.com/muraliprajapati/typeorm-pglite) documentation for
more details.
