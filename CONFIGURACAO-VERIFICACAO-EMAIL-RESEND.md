# LiDire — Verificação de e-mail com Resend

## Como funciona

1. No cadastro, a conta é criada como pendente e a LiDire envia um link de confirmação.
2. O link expira em 24 horas e só pode ser usado uma vez.
3. A pessoa precisa confirmar o endereço antes de conseguir entrar.
4. A tela de autenticação oferece o botão **Reenviar e-mail de confirmação**.
5. Contas anteriores a esta versão não são bloqueadas; a exigência de verificação vale para os novos cadastros.

## Configuração no Cloudflare

No diretório do projeto, execute:

```bash
npx wrangler secret put RESEND_API_KEY
```

Cole sua API Key do Resend quando solicitado. Não coloque a chave no código, no `wrangler.toml` nem em arquivos enviados ao GitHub.

O código usa este remetente padrão:

```text
LiDire <recuperacao@lidire.com>
```

O domínio `lidire.com` e o endereço remetente precisam estar autorizados/verificados na conta Resend. Se quiser usar outro remetente, configure:

```bash
npx wrangler secret put RESEND_FROM_EMAIL
```

Informe o valor completo, por exemplo `LiDire <contato@lidire.com>`, apenas se esse endereço/domínio estiver autorizado no Resend.

## Banco D1

O Worker cria a tabela `email_verification_tokens` e adiciona as colunas de verificação à tabela `users` automaticamente, sem apagar os dados existentes. Não é necessário excluir nem recriar o banco.

## Publicação e teste

1. Publique todos os arquivos no Worker desejado.
2. Faça um cadastro com um e-mail ao qual você tenha acesso.
3. Confira a caixa de entrada e a pasta Spam/Lixo eletrônico.
4. Abra o link de confirmação recebido.
5. Volte à LiDire e entre com o mesmo e-mail e senha.

Se o e-mail não chegar, use **Reenviar e-mail de confirmação** e confira os logs do Worker. Nunca compartilhe a API Key do Resend.
