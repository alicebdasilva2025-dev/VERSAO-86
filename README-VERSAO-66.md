# LiDire — Versão 66

## Correções e melhorias

### 1. Compromissos visíveis e disponíveis para a IA
- A tela do Assistente agora exibe os próximos quatro compromissos futuros cadastrados na Agenda, com data, horário e local/endereço quando disponível.
- O contexto enviado ao Gemini inclui explicitamente os campos de agenda, inclusive o endereço do compromisso, para que a IA consiga responder perguntas sobre eventos cadastrados e calcular rotas para eles.
- O backend orienta a IA a consultar os compromissos presentes no contexto e a pedir esclarecimento se faltarem dados ou houver mais de um compromisso possível.

### 2. Exclusão de lembrete sem rolar para o topo
- Ao excluir um lembrete, a tela é renderizada preservando a posição de rolagem atual.

### 3. Endereço residencial no Perfil
- A tela de Perfil exibe o endereço de casa e um atalho para cadastrá-lo ou editá-lo.
- O campo já é persistido pelo endpoint `/api/profile` e a versão mantém essa integração.
- O endereço residencial é enviado separadamente no contexto da IA; o sanitizador geral continua excluindo endereços de outros registros, exceto o endereço explicitamente selecionado do perfil e os endereços da agenda necessários para rotas.
- Quando a IA solicita uma rota usando “casa”, “minha casa” ou expressões equivalentes, o aplicativo resolve o termo para o endereço residencial cadastrado, como origem ou destino conforme a frase.

## Arquivos alterados
- `app.js`
- `index.js`

## Verificações
- Sintaxe verificada com `node --check` para `app.js` e `index.js`.
- Não foi feito deploy nem teste integrado com a conta Cloudflare/Google do usuário; testar em ambiente de homologação antes de publicar.
