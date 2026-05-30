# O que aprendi aqui

## Execução de código

Aparentemente, executar arquivos soltos em GO é tão simples quanto executar um `go run [nomedoarquivo].go`.
Entretanto, descobri que existe um tal de go mod init, que inicializa um módulo go, que é similar ao npm init ou ao pyproject.toml

Sintaxe:
`go mod init <nome-do-modulo>`

O nome do módulo é o "endereço" pelo qual outros pacotes vão importar o seu código. A convenção é usar o caminho do repositório:

`go mod init github.com/jsarti/go-lang-studies`

Isso cria um `go.mod` assim:

```
module github.com/jsarti/go-lang-studies

go 1.26.3
```

Na prática, o nome importa em dois cenários:

Se for uma lib pública, o nome precisa bater com a URL real do repo, senão go get não funciona para quem instalar.
Se for código interno/estudos, pode ser qualquer coisa. `go mod init estudos` funciona perfeitamente.

## Padrões em projetos maiores

Em Go, o padrão para monorepo com múltiplas lambdas/serviços é diferente do que você faria em Node.js (onde o workspace do npm amarra tudo).
Opção 1 — Um go.mod por serviço (mais comum em produção)

```
monorepo/
├── services/
│ ├── user-service/
│ │ ├── go.mod ← módulo independente
│ │ └── main.go
│ ├── order-service/
│ │ ├── go.mod
│ │ └── main.go
│ ├── payment-service/
│ ├── go.mod
│ └── main.go
├── shared/
├── go.mod ← lib interna compartilhada
├── pkg/
├── logger/
└── errors/
```

Cada serviço referencia o shared via replace no seu go.mod:

```
require github.com/jsarti/monorepo/shared v0.0.0

replace github.com/jsarti/monorepo/shared => ../../shared
```

O replace diz "quando importar esse módulo, usa esse caminho local em vez de buscar no registry". Em CI você publicaria o shared com uma tag real e removeria os replace.

Opção 2 — Go Workspace (go work), introduzido no Go 1.18
É o equivalente mais próximo do npm workspaces. Você cria um go.work na raiz que amarra todos os módulos locais sem precisar de replace:

```
# Na raiz do monorepo
go work init
go work use ./services/user-service
go work use ./services/order-service
go work use ./shared

```

Gera um go.work assim:

```
go 1.26.3

use (
./services/user-service
./services/order-service
./services/payment-service
./shared
)
```

A partir daí, qualquer import de github.com/jsarti/monorepo/shared dentro dos serviços é resolvido automaticamente para o caminho local — sem replace em cada go.mod.

```
// dentro de user-service/main.go
import "github.com/jsarti/monorepo/shared/pkg/logger" // resolve local automaticamente
```
