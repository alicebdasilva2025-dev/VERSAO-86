# LiDire — Versão 65

## Sugestão de horário de saída para compromissos

A versão 65 integra a agenda existente à API de rotas para sugerir um horário de saída com base no compromisso cadastrado.

### O que foi implementado
- Na agenda, compromissos com data, horário e endereço exibem a ação **Sugerir horário de saída**.
- O usuário informa a origem, meio de transporte e antecedência desejada.
- A LiDire consulta a integração de rotas existente e calcula uma estimativa de saída.
- O resultado mostra horário sugerido, duração estimada, origem e destino.
- O usuário pode abrir a rota no Google Maps ou Waze usando as integrações já existentes.
- O usuário pode optar por criar um lembrete para sair; o formulário existente de lembretes abre preenchido e exige confirmação antes de salvar.
- O lembrete fica vinculado ao compromisso de origem.
- Para carro e moto, a estimativa faz uma segunda consulta com horário de partida estimado para refinar a previsão de trânsito. Para os demais meios, usa a duração retornada pela primeira consulta.

### Configuração
- Mantém a variável/secret `GOOGLE_MAPS_API_KEY` no Cloudflare Worker.
- Não introduz nova chave de API nem novo serviço pago.
- A função usa os endpoints `/api/routes` e os recursos de lembretes existentes.

### Observações e limites
- O recurso depende de o compromisso ter data, horário e endereço.
- O usuário precisa informar a origem; “Minha localização” pode solicitar permissão de GPS.
- O horário sugerido é uma estimativa e pode mudar conforme trânsito, condições da rota e precisão dos endereços.
- A criação do lembrete não é automática: o usuário revisa e confirma o formulário.
- A integração foi verificada por análise estática e `node --check app.js`. Não foi possível validar chamadas reais às APIs ou notificações no dispositivo sem as credenciais e ambiente de deploy.
