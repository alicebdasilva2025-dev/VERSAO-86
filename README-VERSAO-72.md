# LiDire — Versão 72

## Correção da exportação de dados pessoais

- Substituída a descoberta dinâmica de tabelas via `sqlite_master` e `PRAGMA` por uma lista explícita de tabelas pessoais.
- Cada tabela é consultada apenas por `user_id` da sessão autenticada.
- Tabelas opcionais ausentes ou sem permissão são registradas como ignoradas, sem interromper toda a exportação.
- Campos relacionados a senhas, tokens, sessões, credenciais, chaves e cookies são filtrados.
- Dados de família e tabelas de compartilhamento não fazem parte da lista de exportação.

## Validação
- `node --check index.js`: aprovado.
- O teste funcional precisa ser realizado no Worker publicado, conectado ao D1 real.
