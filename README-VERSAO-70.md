# LiDire — Versão 70

## Exportação de dados pessoais
- Adicionado endpoint autenticado `GET /api/account/export`.
- Adicionado download de arquivo JSON em Perfil > Gerenciamento de dados > Exportar meus dados.
- A exportação inclui apenas registros associados diretamente ao usuário autenticado (`user_id`) e o perfil próprio (`profiles.id`).
- Tabelas de família/compartilhamento, autenticação, tokens, sessões e credenciais são excluídas; campos sensíveis também são filtrados.
- A exportação não exclui nem altera dados do banco.

## Publicação
Publique os arquivos da versão 70 no ambiente Cloudflare usado pela LiDire. O endpoint usa a sessão existente e a binding D1 (`env.DB`).

## Observações de validação
- `app.js` e `index.js` passaram na verificação de sintaxe JavaScript.
- O fluxo de download precisa ser testado no ambiente publicado com uma conta de teste.
- Como o esquema pode variar entre instalações, valide quais tabelas pessoais possuem `user_id` para garantir cobertura integral dos módulos.
