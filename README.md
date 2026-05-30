# go-lang-studies 🐹

Repositório de código de aprendizado de Go — do básico ao avançado. Estruturado em 5 fases progressivas.

> Cada fase tem seu próprio módulo Go, exercícios isolados e um projeto prático que consolida o conteúdo.

---

## Estrutura do repositório

```
go-lang-studies/
├── fase1-fundamentos/
│   ├── 01-tipos-e-variaveis/
│   ├── 02-slices-maps-arrays/
│   ├── 03-structs-e-interfaces/
│   ├── 04-error-handling/
│   ├── 05-funcoes-e-closures/
│   └── projeto-csv-cli/
│
├── fase2-concorrencia/
│   ├── 01-goroutines/
│   ├── 02-channels/
│   ├── 03-sync-primitivos/
│   ├── 04-context/
│   └── projeto-web-crawler/
│
├── fase3-backend/
│   ├── 01-net-http/
│   ├── 02-banco-de-dados/
│   ├── 03-testes/
│   ├── 04-arquitetura/
│   └── projeto-api-rest/
│
├── fase4-sistemas/
│   ├── 01-profiling-e-performance/
│   ├── 02-rede-e-protocolos/
│   ├── 03-cli-e-ferramentas/
│   ├── 04-cloud-native/
│   └── projeto-proxy-reverso/
│
├── fase5-expert/
│   ├── 01-generics/
│   ├── 02-runtime-internals/
│   ├── 03-patterns-avancados/
│   ├── 04-go-em-times/
│   └── projeto-lib-opensource/
│
└── playground/          # experimentos rápidos e rascunhos
```

Cada subdiretório é um módulo Go independente com seu próprio `go.mod`.

---

## Progresso

### Fase 1 — Fundamentos `semanas 1–3`

| Módulo                | Status          | Notas                             |
| --------------------- | --------------- | --------------------------------- |
| Tipos e variáveis     | ⬜ não iniciado | zero values, inferência, pointers |
| Slices, maps e arrays | ⬜ não iniciado | diferenças de valor vs referência |
| Structs e interfaces  | ⬜ não iniciado | composição, duck typing estático  |
| Error handling        | ⬜ não iniciado | errors.Is, errors.As, wrapping    |
| Funções e closures    | ⬜ não iniciado | first-class, variádicas           |
| **Projeto: CSV CLI**  | ⬜ não iniciado | lê, filtra, agrupa e exporta      |

### Fase 2 — Concorrência `semanas 4–7`

| Módulo                   | Status          | Notas                                    |
| ------------------------ | --------------- | ---------------------------------------- |
| Goroutines               | ⬜ não iniciado | scheduler M:N, GOMAXPROCS, leaks         |
| Channels                 | ⬜ não iniciado | buffered, select, pipeline, fan-out      |
| sync e primitivos        | ⬜ não iniciado | WaitGroup, Mutex, Once, atomic           |
| Context                  | ⬜ não iniciado | cancelamento, timeout, shutdown graceful |
| **Projeto: Web Crawler** | ⬜ não iniciado | concorrente com worker pool              |

### Fase 3 — Backend real `semanas 8–13`

| Módulo                | Status          | Notas                                |
| --------------------- | --------------- | ------------------------------------ |
| net/http              | ⬜ não iniciado | handlers, middleware, ServeMux 1.22+ |
| Banco de dados        | ⬜ não iniciado | database/sql, sqlx, SQLC, migrations |
| Testes                | ⬜ não iniciado | table-driven, fuzz, benchmarks       |
| Arquitetura           | ⬜ não iniciado | DI manual, repository pattern, slog  |
| **Projeto: API REST** | ⬜ não iniciado | JWT, PostgreSQL, rate limiting       |

### Fase 4 — Programação de sistemas `semanas 14–20`

| Módulo                     | Status          | Notas                                       |
| -------------------------- | --------------- | ------------------------------------------- |
| Performance e profiling    | ⬜ não iniciado | pprof, trace, escape analysis, sync.Pool    |
| Rede e protocolos          | ⬜ não iniciado | TCP/UDP raw, gRPC, WebSockets               |
| CLI e ferramentas          | ⬜ não iniciado | Cobra, Bubbletea, cross-compilation         |
| Cloud native               | ⬜ não iniciado | Docker multi-stage, OpenTelemetry, k8s      |
| **Projeto: Proxy reverso** | ⬜ não iniciado | load balancing, circuit breaker, Prometheus |

### Fase 5 — Expert `semanas 21–26`

| Módulo                       | Status          | Notas                                        |
| ---------------------------- | --------------- | -------------------------------------------- |
| Generics                     | ⬜ não iniciado | type params, constraints, stdlib slices/maps |
| Runtime internals            | ⬜ não iniciado | GC, G/M/P model, memory model, unsafe        |
| Patterns avançados           | ⬜ não iniciado | functional options, iterators, CQRS          |
| Go em times                  | ⬜ não iniciado | API design, go/analysis, godoc, semver       |
| **Projeto: Lib open-source** | ⬜ não iniciado | API estável, fuzz, CI, goreleaser            |

> **Legenda:** ⬜ não iniciado · 🔄 em progresso · ✅ concluído

---

## Como rodar os exemplos

Pré-requisitos: Go 1.26+, Git.

```bash
# Clona o repo
git clone https://github.com/seu-usuario/go-lang-studies.git
cd go-lang-studies

# Entra em qualquer exercício e roda
cd fase1-fundamentos/01-tipos-e-variaveis
go run .

# Roda os testes de um módulo
go test ./...

# Roda com race detector (hábito desde a fase 2)
go test -race ./...
```

Cada diretório de exercício tem um `README.md` próprio explicando o que está sendo explorado e por quê.

---

## Filosofia de estudo

Alguns princípios que guiam este repositório:

**Erros como valores, não exceções.** Go não tem `try/catch`. Cada função retorna o erro explicitamente — isso força a lidar com falhas onde elas acontecem.

**Composição em vez de herança.** Não existe classe base em Go. Structs se compõem por embedding e interfaces são implementadas implicitamente — duck typing com verificação estática.

**Concorrência por comunicação.** _"Do not communicate by sharing memory; instead, share memory by communicating."_ Channels antes de mutexes. Goroutines antes de thread pools.

**Simplicidade é expertise.** Não usar generics quando interfaces bastam. Não usar goroutines quando código sequencial é mais claro. A stdlib vai longe — lib externa só quando ela não chega.

---

## Recursos de referência

| Recurso                                                                     | Fase | Tipo       |
| --------------------------------------------------------------------------- | ---- | ---------- |
| [Tour of Go](https://go.dev/tour/)                                          | 1    | interativo |
| [Go by Example](https://gobyexample.com/)                                   | 1–2  | referência |
| [Effective Go](https://go.dev/doc/effective_go)                             | 1–2  | leitura    |
| [Concurrency Patterns](https://go.dev/blog/concurrency-patterns)            | 2    | blog       |
| [Pipelines in Go](https://go.dev/blog/pipelines)                            | 2    | blog       |
| [Let's Go](https://lets-go.alexedwards.net/) — Alex Edwards                 | 3    | livro      |
| [Let's Go Further](https://lets-go-further.alexedwards.net/) — Alex Edwards | 3–4  | livro      |
| [pprof guide](https://go.dev/blog/pprof)                                    | 4    | blog       |
| [100 Go Mistakes](https://100go.co/) — Teiva Harsanyi                       | 4–5  | livro      |
| [Go Memory Model](https://go.dev/ref/mem)                                   | 5    | spec       |
| [Go spec](https://go.dev/ref/spec)                                          | 1–5  | referência |

---

## Ambiente de desenvolvimento

- **OS:** Ubuntu 24.04 via WSL2
- **Go:** 1.26.3
- **Editor:** VSCode com extensão `golang.go` e gopls
- **Linter:** golangci-lint
- **Formatter:** gofumpt (via gopls)

---

## Licença

MIT — código de aprendizado, use à vontade.
