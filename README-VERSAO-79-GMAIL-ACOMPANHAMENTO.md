# LiDire — Versão 79: acompanhamento de e-mails importantes

## Implementado nesta versão
- Cadastro de remetentes importantes por endereço, categoria (Trabalho, Estudos, Pessoal ou Financeiro), prazo de 6/12/24 horas e preferência de aviso ao receber.
- Persistência de regras e acompanhamento no D1, sem recriar ou apagar dados existentes.
- Rotina agendada do Worker a cada 15 minutos para consultar a caixa de entrada dos usuários com remetentes cadastrados, registrar mensagens novas e identificar respostas enviadas posteriormente na mesma conversa.
- Resumo na página inicial para acompanhamentos vencidos e botão para revisar e-mails.
- Preservação da conexão Gmail OAuth e da revisão manual já existente.

## Deploy
- Publique os arquivos do ZIP no Worker correto e preserve o binding D1 `DB`, os segredos Google e o domínio atual.
- O `wrangler.toml` inclui cron `*/15 * * * *`. Se o deploy for feito pelo editor do painel, confirme em Settings/Triggers que a rotina cron está configurada; publicar arquivos manualmente pode não atualizar os gatilhos.
- As tabelas de acompanhamento são criadas automaticamente pelo Worker no primeiro uso. Não execute DROP e não substitua o banco.

## Limitações importantes
- A rotina verifica e-mails periodicamente, não em tempo real. O prazo é contado a partir da data da mensagem e a revisão ocorre em ciclos de até 15 minutos.
- O resumo diário mostra acompanhamentos vencidos quando a página inicial é aberta. O recurso ainda não envia notificações push ou alertas de recebimento fora do aplicativo; a preferência de aviso de novo e-mail fica armazenada, mas entrega de notificação em segundo plano exige uma etapa futura (por exemplo, Web Push com inscrição do dispositivo).
- A detecção de resposta verifica mensagens enviadas na mesma conversa. Ela pode não reconhecer respostas enviadas em outro thread ou por outro cliente/conta.
- Teste com mensagens controladas antes de usar como acompanhamento crítico. A classificação não garante que uma mensagem realmente precise de resposta.
