# SiYuan CLI — Full Command Reference

Auto-generated from `siyuan --help` output (v3.7.0-dev14).

---

## Top-Level Flags

These flags are available on every subcommand (global flags):

| Flag | Description |
|------|-------------|
| `-f, --format <table\|json>` | Output format (default: `table`) |
| `-h, --help` | Show help |
| `-v, --version` | Print version |
| `-w, --workspace <path>` | Workspace path (required for all commands except `workspace`) |
| `--dry-run` | Dry run mode: validate and print what would happen without making changes |

> **Note:** All global flags except `-w` (or `--workspace`) are optional. The CLI will use default values if optional flags are not specified.

---

## workspace — Manage Workspaces

```
siyuan workspace [command]
```

### Subcommands
| Command | Description |
|---------|-------------|
| `list` | List registered workspaces |
| `info` | Show current workspace info |

### Example
```bash
siyuan workspace list
siyuan workspace info
```

---

## notebook — Manage Notebooks

```
siyuan notebook [command] -w <path>
```

### Subcommands
| Command | Flags | Description |
|---------|-------|-------------|
| `list` | | List all notebooks |
| `create` | `--name <name>` | Create a notebook (ID auto-generated) |
| `open` | `--id <id>` | Open a notebook |
| `close` | `--id <id>` | Close a notebook |
| `rename` | `--id <id> --name <name>` | Rename a notebook |
| `remove` | `--id <id>` | Remove a notebook |

---

## document — Manage Documents

```
siyuan document [command] -w <path>
```

### Subcommands
| Command | Description |
|---------|-------------|
| `list` | List documents in a notebook |
| `get` | Get document info |
| `create` | Create a document |
| `rename` | Rename a document |
| `move` | Move a document to another notebook |
| `duplicate` | Duplicate a document |
| `remove` | Remove a document |

---

## block — Block Operations

```
siyuan block [command] -w <path>
```

### Subcommands
| Command | Flags | Description |
|---------|-------|-------------|
| `get` | `--id <id>` | Get block info |
| `children` | `--id <id>` | Get child blocks |
| `insert` | `--id <id>` | Insert block |
| `append` | `--id <id>` | Append block |
| `prepend` | `--id <id>` | Prepend block |
| `stat` | | Get block content statistics |
| `update` | `--id <id>` | Update block |
| `delete` | `--id <id>` | Delete block |
| `move` | `--id <id>` | Move block |
| `dom` | `--id <id>` | Get block DOM |
| `kramdown` | `--id <id>` | Get block kramdown |
| `breadcrumb` | `--id <id>` | Get block breadcrumb |
| `batch-get` | `--ids <ids>` | Batch get block info |
| `batch-kramdown` | `--ids <ids>` | Batch get block kramdown |

---

## sql — Execute SQL Query

```
siyuan sql "<statement>" [flags] -w <path>
```

### Flags
| Flag | Description |
|------|-------------|
| `-l, --limit <int>` | Max rows returned (default: 100) |

### Example
```bash
siyuan sql "SELECT * FROM blocks WHERE type='document' LIMIT 10" -w /path -f json
```

---

## search — Full-Text Search

```
siyuan search <query> [flags] -w <path>
```

### Flags
| Flag | Description |
|------|-------------|
| `-m, --method <int>` | 0=keyword 1=query-syntax 2=sql 3=regex 4=fuzzy |
| `-t, --type <stringArray>` | Block type filter (repeatable) |
| `--subtype <stringArray>` | Block subtype filter (repeatable) |
| `-n, --notebook <stringArray>` | Notebook ID filter (repeatable) |
| `--path <stringArray>` | Path prefix filter (repeatable) |
| `-o, --order-by <int>` | 0=type 1=created-asc 2=created-desc 3=updated-asc 4=updated-desc 5=content 6=relevance-asc 7=relevance-desc |
| `-p, --page <int>` | Page number (default: 1) |
| `-s, --page-size <int>` | Results per page (default: 32) |
| `-g, --group-by <int>` | 0=none 1=document |

> **Note:** `-m 4` (fuzzy/vector search) requires an embedding model to be configured in SiYuan settings and embeddings to be generated before use. If results are empty or an error occurs, prompt the user to configure the embedding model first.

### Block Types for `-t`
`document heading paragraph list listItem codeBlock mathBlock table blockquote superBlock htmlBlock embedBlock databaseBlock audioBlock videoBlock iframeBlock widgetBlock callout`

---

## export — Export Documents

```
siyuan export [command] -w <path>
```

### Subcommands
| Command | Flags | Description |
|---------|-------|-------------|
| `md --id <id> [--output <path>]` | | Export as Markdown (default: stdout) |
| `html` | | Export as HTML |
| `docx` | | Export as Word (.docx) |
| `sy` | | Export as .sy.zip |
| `md-zip` | | Export as Markdown zip |
| `preview` | | Export as preview HTML |
| `data` | | Export full workspace data backup |

---

## import — Import Files

```
siyuan import [command] -w <path>
```

### Subcommands
| Command | Flags | Description |
|---------|-------|-------------|
| `md --file <path> --notebook <id>` | `--hpath <path>` `--path <path>` | Import Markdown file or directory |
| `sy` | | Import .sy.zip archive |
| `data` | | Import data backup |

---

## asset — Manage Assets

```
siyuan asset [command] -w <path>
```

### Subcommands
| Command | Flags | Description |
|---------|-------|-------------|
| `unused` | | List unused assets |
| `clean` | | Clean unused assets |
| `stat` | `--path <path>` | Show asset file info |
| `upload` | | Upload files to workspace assets |

---

## attr — Manage Block Attributes

```
siyuan attr [command] -w <path>
```

### Subcommands
| Command | Description |
|---------|-------------|
| `get --id <id>` | Get block attributes |
| `set` | Set block attributes |
| `batch-get` | Batch get block attributes |

---

## bookmark — Manage Bookmarks

```
siyuan bookmark [command] -w <path>
```

### Subcommands
| Command | Description |
|---------|-------------|
| `list` | List bookmarks |
| `labels` | List bookmark labels |
| `rename` | Rename a bookmark |
| `remove` | Remove a bookmark |

---

## tag — Manage Tags

```
siyuan tag [command] -w <path>
```

### Subcommands
| Command | Description |
|---------|-------------|
| `list` | List tags |
| `rename` | Rename a tag |
| `remove` | Remove a tag |

---

## history — Data History

```
siyuan history [command] -w <path>
```

### Subcommands
| Command | Description |
|---------|-------------|
| `list` | List all history |
| `get` | Get historical file content |
| `search` | Search history |
| `rollback` | Rollback a document to historical version |
| `clear` | Clear all history |

---

## ref — Backlinks and References

```
siyuan ref [command] -w <path>
```

### Subcommands
| Command | Flags | Description |
|---------|-------|-------------|
| `backlinks --id <id>` | `--keyword <str>` `--sort <int>` | Get backlinks for a block |
| `mentions --id <id>` | `--keyword <str>` `--sort <int>` | Get mentions for a block |
| `refresh --id <id>` | | Refresh backlinks for a block |

### Sort values for backlinks/mentions
0=updated-desc 1=updated-asc 2=created-desc 3=created-asc 4=name-desc 5=name-asc 6=alphanum-desc 7=alphanum-asc

---

## repo — Data Snapshots

```
siyuan repo [command] -w <path>
```

### Subcommands
| Command | Description |
|---------|-------------|
| `list` | List snapshots |
| `create` | Create a snapshot |
| `diff` | Diff two snapshots |
| `checkout` | Checkout (rollback to) a snapshot |
| `tag` | `--id <id> --name <name>` | Tag a snapshot |
| `untag` | `--name <name>` | Remove a tag |
| `purge` | Purge old snapshots |
| `search` | Search files in snapshots |
| `file` | File-level snapshot operations (export/get/open/rollback) |

---

## sync — Sync with Cloud

```
siyuan sync [flags] -w <path>
siyuan sync [command] -w <path>
```

### Subcommands
| Command | Description |
|---------|-------------|
| `pull` | Download from cloud |
| `push` | Upload to cloud |
| `status` | Show sync status |

---

## database — Manage Databases (Attribute Views)

```
siyuan database [command] -w <path>
```

### Subcommands
| Command | Description |
|---------|-------------|
| `search` | Search databases by name |
| `get` | Get database content |
| `keys` | List database keys (fields) |
| `key add` | Add a key (field) to database |
| `key remove` | Remove a key (field) from database |
| `item add` | Add a row to database |
| `item update` | Update a cell value |
| `item remove` | Remove rows from database |
| `render` | Render database data |
| `unused` | List unused databases |
| `clean` | Clean unused databases |

---

## dailynote — Daily Note Operations

```
siyuan dailynote [command] -w <path>
```

### Subcommands
| Command | Flags | Description |
|---------|-------|-------------|
| `create --notebook <id>` | | Create today's daily note |
| `append --notebook <id> [--data <md>\|--file <path>]` | `--data` `--file` (`-` for stdin) | Append block to today's daily note |
| `prepend --notebook <id> [--data <md>\|--file <path>]` | `--data` `--file` (`-` for stdin) | Prepend block to today's daily note |

---

## file — Workspace File Operations

```
siyuan file [command] -w <path>
```

### Subcommands
| Command | Flags | Description |
|---------|-------|-------------|
| `list --path <path>` | | List directory contents |
| `read --path <path>` | | Read file content |
| `write <path> [--file <src>]` | `--file <src>` | Write file content (from stdin or file) |
| `copy --src <src> --dst <dst>` | | Copy file or directory |
| `rename --old <old> --new <new>` | | Rename or move file |
| `delete --path <path>` | | Delete file or directory |
| `find --path <path>` | `--pattern <pattern>` | Find files under a path |
| `grep --path <path>` | `--pattern <pattern>` | Search file contents with regex |
| `stat --path <path>` | | Show file or directory info |

---

## outline — Document Outline

```
siyuan outline [command] -w <path>
```

### Subcommands
| Command | Flags | Description |
|---------|-------|-------------|
| `get --id <id>` | `--id <id>` | Get document outline (heading tree) |

---

## system — System Information

```
siyuan system [command] -w <path>
```

### Subcommands
| Command | Description |
|---------|-------------|
| `current-time` | Show current server time |

---

## template — Manage Templates

```
siyuan template [command] -w <path>
```

### Subcommands
| Command | Flags | Description |
|---------|-------|-------------|
| `search [keyword]` | | Search templates; empty keyword lists all |
| `get --path <path>` | `--path <path>` | Read template content |
| `create --name <name>` | `--name <name>` `--data <md>` `--file <path>` (`-` for stdin) `--overwrite` | Create template from markdown content |
| `save-as --id <id> --name <name>` | `--id <id>` `--name <name>` `--overwrite` | Save a document as a template |
| `render --path <path> --id <id>` | `--path <path>` `--id <id>` | Render template against a block (preview) |
| `remove --path <path>` | `--path <path>` | Remove a template |

> `--path` accepts absolute path or path relative to `data/templates/` in the workspace.

---

## serve — Start Kernel HTTP Server

```
siyuan serve [flags]
```

Starts the SiYuan kernel HTTP server for API access.

### Flags
| Flag | Description |
|------|-------------|
| `--workspace <path>` | Workspace path (optional, defaults to default workspace if not specified; note: only full form `--workspace`, not `-w`) |
| `--accessAuthCode <string>` | Access auth code |
| `--attach-ui` | Attach kernel lifecycle to desktop UI process (used by Electron) |
| `--lang <string>` | Language: ar/de/en/es/fr/he/hi/id/it/ja/ko/nl/pl/pt-BR/ru/sk/th/tr/uk/zh-CN/zh-TW |
| `--mode <string>` | Run mode: dev/prod (default "prod") |
| `--port <string>` | Port of the HTTP server (default "0" = auto) |
| `--readonly <string>` | Read-only mode: true/false (default "false") |
| `--ssl` | Enable HTTPS and WSS |
| `--wd <string>` | Working directory of SiYuan |

> **Note:** `serve` does not require `-w` flag; it starts the kernel which then loads the workspace.

---

## completion — Generate Shell Completion

```
siyuan completion [command]
```

### Subcommands
| Command | Description |
|---------|-------------|
| `bash` | Generate autocompletion script for bash |
| `fish` | Generate autocompletion script for fish |
| `powershell` | Generate autocompletion script for powershell |
| `zsh` | Generate autocompletion script for zsh |

Generate autocompletion script for the specified shell.
