# LiDire — Versão 82

## Correção de confirmação de e-mail
- Corrige a consulta da rota `/api/email/verification/resend`: a coluna `email` agora é incluída no `SELECT`, pois a função usava `user.email` sem ter selecionado esse campo. Isso causava o envio de `to: [null]` ao Resend.
- Valida o destinatário antes de criar/rotacionar tokens de confirmação e antes de chamar o Resend.
- Valida caracteres não ASCII no remetente e no endereço do destinatário para evitar requisições inválidas ao provedor.
- Não altera o esquema nem apaga dados do D1.

## Testes realizados
- `node --check index.js`
- `node --check app.js`
- Revisão da consulta SQL da rota de reenvio e do payload enviado ao Resend.

## Antes de publicar
- Preserve o banco D1 existente (`lidire-mvp-db`); não execute scripts para recriar tabelas nem apagar registros.
- Confirme que os secrets/vars necessários estão presentes no Worker de destino, especialmente `RESEND_API_KEY` e `RESEND_FROM_EMAIL`.
- O `wrangler.toml` ainda possui o nome antigo `director` e um Cron trigger. Ajuste o nome conforme o pipeline de deploy e confira o limite de Cron da conta antes de publicar; esta entrega não altera os gatilhos nem resolve o limite da conta.
- Depois do deploy, teste o reenvio de confirmação com um cadastro pendente e confirme no Resend que `to` contém o endereço real, não `null`.
- Teste separadamente a recuperação de senha. Esta correção trata a rota de reenvio de confirmação de cadastro; não garante por si só que todos os fluxos de e-mail estejam corrigidos.
