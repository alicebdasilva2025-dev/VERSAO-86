# LiDire — Versão 78: integração Gmail (somente leitura)

## O que foi adicionado
- Conexão OAuth com uma conta Google/Gmail a partir do Perfil > Conectividade.
- Tokens OAuth protegidos por AES-GCM antes de serem gravados no D1; a chave é lida do segredo `GOOGLE_TOKEN_ENCRYPTION_KEY`.
- Consulta das mensagens recentes da caixa de entrada (metadados e trecho), sem permissão de enviar, apagar ou modificar mensagens.
- Sugestão heurística de e-mails que talvez precisem de resposta.
- Ação explícita para criar um lembrete local para o dia seguinte às 09:00. A LiDire não envia respostas automaticamente.
- Botão para desconectar Gmail.

## Configuração necessária no Cloudflare
No Worker de produção que atende `https://app.lidire.com`, confirme:
- `GOOGLE_CLIENT_ID` (variável)
- `GOOGLE_CLIENT_SECRET` (segredo)
- `GOOGLE_TOKEN_ENCRYPTION_KEY` (segredo aleatório forte, não compartilhe)
- Binding D1 `DB` já existente

## Configuração necessária no Google Cloud
No cliente OAuth do tipo Aplicativo da Web, adicione em **URIs de redirecionamento autorizados** exatamente:
`https://app.lidire.com/api/connections/gmail/callback`

Mantenha também a origem JavaScript autorizada `https://app.lidire.com` se o cliente existente a utiliza para o botão de login Google.
Ative a **Gmail API** no projeto Google Cloud e configure a tela de consentimento OAuth. O escopo solicitado é `https://www.googleapis.com/auth/gmail.readonly` (além de `openid email`). Enquanto o app estiver em modo de teste, inclua a conta Google usada no teste como usuário de teste. A disponibilização pública desse escopo pode exigir verificação do Google.

## Teste
1. Faça deploy do conteúdo deste ZIP no Worker correto, mantendo o binding D1 `DB` e o domínio `app.lidire.com`.
2. Confirme as três configurações do Worker acima.
3. Adicione o URI de redirecionamento no Google Cloud e ative a Gmail API.
4. Entre na LiDire, abra Perfil > Conectividade > Conectar Gmail e aceite as permissões.
5. Use **Revisar e-mails** e crie um lembrete de teste. A classificação de resposta é apenas uma sugestão e pode errar.

A conexão não será funcional até que as configurações externas e o deploy sejam concluídos.
