# Command Catalog Seed

This file captures repeatable commands observed in the reference environments so they can later be promoted into repo templates and skills.

## PROJECT1 / ExampleServer

- lint: `nox -s lint`
- fast validation: `nox -s fast`
- broad validation: `nox -s all`
- targeted pytest: `nox -s pytest -- tests/test_smoke.py`
- integration tests: `nox -s integration`
- local export flow: `nox -s local-export-flow`
- export artifact validation: `nox -s export-artifact -- /path/to/export.zip`

## PROJECT1 / ExampleViewer

- lint / format check: `npm run format:check`
- build: `npm run build`
- e2e: `npm run test:e2e -- <spec>`
- e2e install: `npm run test:e2e:install`

## PROJECT2 / ExampleBackend

- lint: `python -m nox -s lint`
- tests: `python -m nox -s tests`
- Docker compose stack: `docker compose -f compose.local.yml --env-file .env.local up --build -d db api`
- seed data: `docker compose -f compose.local.yml --env-file .env.local run --rm seed`
- compose tests: `docker compose -f compose.local.yml --env-file .env.local run --rm tests`
- compose smoke: `docker compose -f compose.local.yml --env-file .env.local run --rm smoke`
- compose teardown: `docker compose -f compose.local.yml --env-file .env.local down -v --remove-orphans`

## PROJECT2 / ExampleFrontend

- lint: `npm run lint`
- tests: `npm run test`
- typecheck: `npm run typecheck`
- build: `npm run build`
- e2e: `npm run test:e2e -- <spec>`

## How To Use This Catalog

- Copy the relevant commands into a new repo's command inventory.
- Replace the examples with the repo's actual entrypoints and ports.
- Promote the stable commands into skills only after the inventory is settled.
