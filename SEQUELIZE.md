# Sequelize Errors

A collection of Sequelize errors.

## Sequelize: TypeError: Cannot read property `replace` of undefined

Typically seen when Sequelize is attempting to read a variable taken from the
environment (like a `.env` file through the `dotenv` command). If the
environment variables are unavailable, then Sequelize will end up attempting to
call the `replace` method on `undefined`.

You can check for the existence of the environment variables that are being used
by placing a `console.log(config)` near the top of the `config/database.js`
file to examine the `config` object imported from the `config/index.js` file.

Sometimes, the student has just forgotten the `dotenv` part of the `db:`
commands. Sometimes, it might be a little more than that.

## Sequelize tells you to install the `mysql2` package

If the `.sequelizerc` file was made after running the `npx sequelize init`
command, or was placed in the wrong location when running that command, then the
generated files will be at the default location for Sequelize and look for
a `config.json` file. This can easily be remedied by removing the files and
directories created by the `init` command, recreating the `.sequelizerc` in the
right place with the right contents, and re-running the `npx sequelize init`
command, or by moving the files and properly updating the `models/index.js` file
to find the right config file. For the purposes of Authenticate Me, the config
variable should point to the `config/database.js` file in the `backend`
directory.

## Something about a column not existing

Check the associations for a column name that doesn't exist on the right model.

* Foreign keys on a `belongsTo` should exist on the current model.
* Foreign keys on a `hasOne` or `hasMany` should exist on the opposing model.

Occasionally, you might find a typo on a column name.

## `update or delete ... violates constraints`

Check the associations. If they have the `onDelete: 'cascade', hooks: true`
portion in their association object, remember that the individual hook only
fires when the instance method version of `.destroy()` or `.update()` is used.
They can query with a `.findByPk()` to get the row to destroy or update, and
call the instance method on that instance.

Make sure that the `onDelete: 'cascade', hooks: true` settings are only on the
association object on one side if the association. If you have them on both
sides, you'll cause recursive loops of SQL queries.

## `.findByPk` query doesn't return a row

If they're getting the `id` that they're using to query with from `req.params`,
check to see if they've converted that value to a Number type before querying
with it.

## Sequelize looks for a database on port `3306`

One of two potential issues:

1. Line 8 on the `backend/db/models/index.js` file might not be pointing to the
   `backend/config/database.js` file.
2. The `backend/config/database.js` might not have the correct `dialect` key for
   the environment.

## Sequelize can't connect to `5423`

Postgres might not be running. Check the status of Postgres and if it's not
running, start the instance.

On MacOS, if Postgres was instaleld with Homebrew, you can run

```bash
brew services start postgresql
```

On WSL, you can run

```bash
sudo service postgresql start
```
