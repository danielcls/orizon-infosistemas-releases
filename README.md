# Orizon InfoSistemas — Releases

Repositório **público**, contendo **somente as releases** (instaladores) do sistema Orizon InfoSistemas.
**Não há código-fonte aqui** — o código vive em repositório privado separado.

## Por que este repositório existe

O atualizador automático (OTA) do sistema consulta a GitHub Releases API:

```
GET https://api.github.com/repos/danielcls/orizon-infosistemas-releases/releases/latest
```

Como este repositório é **público**, qualquer instalação do sistema baixa as atualizações
**sem precisar de token** — e nenhum segredo é distribuído nas máquinas dos clientes.
Manter as releases aqui permite que o repositório de **código permaneça privado** sem quebrar o OTA.

## O que cada release contém

Cada release publica:

- **`OrizonSGC-Setup-v{Major}.{Minor}.{Build}.exe`** — instalador (asset que o OTA baixa)
- **`SHA256SUMS.txt`** — hash SHA-256 do instalador (verificação de integridade)
- Notas da versão no corpo da release

A tag segue o formato `v{Major}.{Minor}.{Build}` (ex.: `v1.0.2`).

## Como publicar uma nova versão

No repositório de código, com o instalador já gerado em `dist\`:

```powershell
.\tools\publish-release.ps1 -Version "1.0.2" -Notes "Correções e melhorias"
```

O script compila o instalador (se necessário), calcula o SHA-256 e cria a release
neste repositório com o asset anexado. Requer `gh` (GitHub CLI) autenticado.

## Segurança

- Este repositório **nunca** deve receber código-fonte, `appsettings` com segredos, certificados ou chaves.
- O token do repositório **privado** de código **nunca** deve ser colocado no `appsettings` dos clientes.
