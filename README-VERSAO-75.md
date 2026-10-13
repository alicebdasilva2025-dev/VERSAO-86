# LiDire — Versão 75

## Correções
- Corrige o horário de geração do relatório para exibir o horário de Brasília (America/Sao_Paulo).
- A exportação tenta identificar diferentes nomes de coluna de titularidade (`user_id`, `owner_user_id`, `created_by_user_id`, `account_id` e `profile_id`) antes de marcar uma tabela como indisponível.
- Mantém a exclusão de credenciais, tokens, sessões e identificadores técnicos internos.
- Tabelas sem uma coluna de titularidade reconhecida não são exportadas, para evitar misturar dados de outras pessoas ou dados compartilhados da família.

## Importante
A lista final de categorias exportadas depende das tabelas e colunas existentes no banco D1 em produção. Após publicar esta versão, gere um novo PDF e confira o aviso de categorias não incluídas.
