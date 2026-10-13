# Correção: familiares não aparecem após login

## Causa identificada
A interface consultava `/api/family/check-email` ao verificar o e-mail, mas não carregava a lista completa com `GET /api/family` ao entrar na conta. Por isso o servidor podia reconhecer o cadastro no D1 e a interface ainda não exibir o familiar, especialmente em outro dispositivo ou após novo login.

## Alteração
- Adicionada `loadFamilyFromD1()` para buscar os membros associados ao grupo familiar da conta autenticada.
- A função é chamada após login/criação de conta e ao restaurar uma sessão existente.
- Registros vindos do D1 são normalizados e mesclados com rascunhos locais não sincronizados.
- A lista local não é apagada se a consulta ao servidor falhar.

## Teste necessário
Publicar e entrar na conta que cadastrou o familiar; conferir a área Família. Confirmar também que a mesma conta vê os membros em outro navegador/dispositivo. A validação local de sintaxe não substitui o teste com o D1 real.
