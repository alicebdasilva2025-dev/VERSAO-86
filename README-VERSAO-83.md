# LiDire — Versão 83

## Correção de notificações da família
- Corrige gravações em `family_notifications` para preencher `family_member_id`, campo obrigatório presente no banco D1 em produção.
- Aplica o vínculo do membro nos fluxos de notificação de convite pendente, convite aceito/recusado e envio manual de notificação.
- Garante que a inicialização da tabela reconheça `family_member_id` em instalações que ainda não possuem essa coluna.
- Preserva o banco D1 e os registros existentes; não apaga membros, convites nem notificações.

## Validação realizada
- `node --check index.js`
- `node --check app.js`
- Revisão dos cinco pontos de gravação em `family_notifications` para garantir que todos incluam `family_member_id`.

## Antes de publicar
- Faça deploy para o Worker correto (`versao-82` ou o nome usado pelo seu pipeline) somente após conferir o destino.
- Preserve o banco D1 existente (`lidire-mvp-db`); não recrie nem apague tabelas ou registros.
- Após publicar, teste o envio de notificação para um membro com conta LiDire e confira se a chamada `POST /api/family/notifications` retorna sucesso.
- Teste também aceitar/recusar convite e cadastrar um familiar já registrado, pois esses fluxos também gravam notificações.

Esta versão foi validada estaticamente; não foi implantada nem testada contra o banco D1 de produção nesta sessão.
