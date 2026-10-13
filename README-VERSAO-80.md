# LiDire — Versão 80

## Alterações desta versão
- Botão “PEDIR AJUDA À LIDIRE” em caixa alta, com gradiente oficial roxo → azul → ciano, contraste e foco visível.
- Resumo diário na tela inicial com texto conversacional em primeira pessoa/voz de assistente, usando dados locais da agenda, tarefas, hidratação e objetivos, sem inventar compromissos.
- Prévia de notificações familiares na tela inicial, com contador de não lidas e ação para marcar como lida. A atualização em segundo plano evita redesenhar a página quando nada mudou.
- Ações rápidas para editar e excluir lembretes diretamente na tela inicial.
- Adicionada a opção de acompanhamento de e-mail após 3 horas (mantidos 6, 12 e 24 horas) no formulário e na validação do Worker.
- Cache do JavaScript atualizado para evitar que o navegador continue carregando o arquivo anterior.

## Bugs anteriores revistos
- **Contador de foco na tela inicial:** o código já sincroniza o valor com o estado do Pomodoro; manter teste de regressão no ambiente publicado.
- **Leitura de Markdown pela voz:** a função `cleanAssistantText` já remove os marcadores mais comuns e a voz usa o texto limpo; validar com respostas reais da IA.
- **Excluir familiar:** o botão e o endpoint DELETE já existem na base 79; testar o fluxo completo com D1.
- **Notificações familiares na inicial:** adicionada visualização e ação de marcar como lida.
- **Lembretes na inicial:** adicionadas ações de editar e excluir.
- **Prazo de 3 horas para e-mail sem resposta:** interface e validação do Worker atualizadas.
- **Status global:** não foi encontrado na renderização atual da tela inicial; não foi necessário remover elemento adicional.

## Ainda precisam de validação ou implementação posterior
- Confirmar ponta a ponta que a IA grava cada registro no módulo correto e que o registro aparece após recarregar a página.
- Confirmar cálculo e persistência de calorias nos alimentos/refeições com testes controlados.
- Testar gráfico de estudos contra os registros de desempenho.
- Verificar consulta de e-mail e cancelamento de lembretes quando uma resposta é detectada.
- Notificações push e alertas em segundo plano ainda não estão implementados nesta versão. A rotina Gmail depende do Cron estar ativo no Worker.
- Confirmar a mensagem de funcionalidade futura para botões de sincronização Google Workspace, Notion e Slack e para consulta de mapas a partir de compromissos.
- Confirmar o convite por e-mail, verificação do cadastro no D1 e sincronização familiar em duas contas reais.

## Publicação segura
- Preserve o Worker, o domínio `app.lidire.com`, o binding D1 `DB` e todos os segredos existentes.
- Não apague nem recrie o D1. Faça backup antes de publicar.
- Verifique no painel Cloudflare se o Cron `*/15 * * * *` continua ativo.
- Esta versão foi submetida a verificação sintática JavaScript; isso não substitui testes funcionais no navegador e no Worker publicado.
