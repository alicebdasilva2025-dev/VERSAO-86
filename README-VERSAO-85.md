# LiDire — Versão 85 — Correção de notificações familiares

- Corrige as gravações de `family_notifications` para incluir `family_member_id`, `resource_type` e `action`.
- Define `action` como `open_family` para notificações de convites e atualizações familiares.
- Atualiza a rotina de compatibilidade para adicionar `resource_type` e `action` quando ausentes, sem apagar tabelas ou registros.
- Atualiza `schema.sql` e `auth-schema.sql` para instalações novas.

Esta versão foi verificada estaticamente. A validação real no D1 de produção ainda deve ser feita em um Worker de teste.
