# yoinked
> a simple, self hosted ip grabber & link shortener

more details to come

## usage
you can run the app after configuring your discord webhook url and admin token, get a template with `cp config.example.ts config.ts`.

you should be able to run it with `deno run ./src/main.ts`, or to pass all permissions, `deno run --allow-env --allow-net --allow-read --allow-write ./src/main.ts`.

### docker
i've build a dockerfile and a compose file for easy running. `docker compose up --build` in the should start it up. `docker compose up --build -d` will detach from the log. bring it down with `docker compose down`.

the database uses a file to store the data `database.json`, so keep that in mind when setting up your docker mounts.

## endpoints

### `GET /`
will show a barebones home page

### `GET /:from`
will 302 redirect you to the destination if it exists, and 404 otherwise

### `GET /expand/:from`
will show destination in plaintext if it exists, and 404 otherwise

### `POST /shorten`, body: `{ from, to }`
will create a shortened link, shortcut and abbreviation must be separated by a `"|"` (`"%7C"`), will respond with 201 on successful add, 422 if a link with that same name already exists, and 400 for other failures

### `POST /enable`, body: `{ from, token }`
will enable yoinking on the selected url if the passeed token matches the configured admin token

