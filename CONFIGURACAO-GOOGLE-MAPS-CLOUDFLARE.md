# Configuração da chave Google Maps no Cloudflare — LiDire 59

A integração com o Google Maps Routes API já está preparada no Worker. O código lê a chave exclusivamente do segredo `GOOGLE_MAPS_API_KEY` (`env.GOOGLE_MAPS_API_KEY`), sem expô-la no navegador.

## Opção 1 — Pelo painel do Cloudflare

1. Entre no painel do Cloudflare.
2. Acesse **Workers & Pages** e abra o Worker usado pela LiDire (o nome deve corresponder ao `name` definido em `wrangler.toml`; neste pacote, `director`).
3. Abra **Settings / Configurações**.
4. Entre em **Variables and Secrets / Variáveis e segredos**.
5. Em **Secrets / Segredos**, escolha para adicionar um novo segredo.
6. Use exatamente este nome: `GOOGLE_MAPS_API_KEY`
7. Cole o valor da chave de API do Google Maps e salve.
8. Faça um novo deploy/redeploy do Worker, se o painel solicitar.

**Importante:** não coloque a chave em `app.js`, `index.js`, `index.html`, `wrangler.toml` ou em qualquer arquivo público. Não a cadastre como variável de frontend/build; ela deve ser um **Secret do Worker em tempo de execução**.

## Opção 2 — Pela linha de comando (Wrangler)

Na pasta do projeto, autentique o Wrangler se necessário e execute:

```bash
npx wrangler secret put GOOGLE_MAPS_API_KEY
```

Quando solicitado, cole a chave e confirme. Depois publique a versão atualizada:

```bash
npx wrangler deploy
```

O comando `secret put` envia a chave diretamente ao Cloudflare como segredo e não precisa gravá-la no projeto.

## APIs e faturamento do Google

No Google Cloud Console, selecione o projeto associado à chave e confirme que a **Routes API** está habilitada e que o projeto tem faturamento configurado, conforme exigido pelo Google. Restrinja a chave de acordo com as recomendações do Google para uso servidor-a-servidor, sem expô-la ao navegador.

## Como verificar

Após salvar o segredo e publicar o Worker:

1. Entre na LiDire.
2. Use uma função que calcule uma rota/tempo de deslocamento.
3. Se a chave não estiver configurada, a API responde com a mensagem `A API de rotas ainda não foi configurada. Adicione GOOGLE_MAPS_API_KEY no Cloudflare.`
4. Se a chave estiver configurada, mas a API do Google não estiver habilitada, não houver faturamento ou a chave estiver restrita incorretamente, o cálculo ainda poderá falhar. Verifique as configurações e permissões no Google Cloud Console.

A rota do Worker utiliza o endpoint `https://routes.googleapis.com/directions/v2:computeRoutes` e lê a chave por `env.GOOGLE_MAPS_API_KEY`.
