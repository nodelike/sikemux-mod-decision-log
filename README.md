# Decision log

A [Sikemux](https://sikemux.com) mod that keeps what your project decided, why, and what it cost. You and your agents write to the same log, so an agent can check it before reopening a question that was already settled.

## Install

Open `sikemux://install-mod?repo=nodelike/sikemux-mod-decision-log`, or install it from [sikemux.com/mods](https://sikemux.com/mods). It installs as `sikemux-mod-decision-log`.

## What it does

- Log a decision with a title, why it was taken, and what spoke against it.
- Mark it proposed, decided, superseded or dropped. The tab's badge counts the proposed ones.
- Filter by status and search titles and reasons.

## Permissions

It reads nothing from Sikemux and writes nothing outside its own data, so it never asks you to allow anything.

## Data

One collection, `decisions`:

| Field | Type | |
| --- | --- | --- |
| `title` | string, up to 200 | required |
| `status` | `proposed`, `decided`, `superseded` or `dropped` | required |
| `why` | string, up to 4000 | |
| `against` | string, up to 4000 | |
| `decidedAt` | integer, milliseconds since 1970 | |

## For agents

Read the log before proposing a change of direction:

```json
mod_read { "mod": "sikemux-mod-decision-log", "collection": "decisions" }
```

Record a decision:

```json
mod_write {
  "mod": "sikemux-mod-decision-log",
  "writes": [{
    "collection": "decisions",
    "id": "d-cache-in-sqlite",
    "set": {
      "title": "Keep the cache in SQLite",
      "status": "decided",
      "why": "One file, no server, fast enough at our size.",
      "against": "No sharing between machines.",
      "decidedAt": 1795000000000
    }
  }]
}
```

## License

MIT
