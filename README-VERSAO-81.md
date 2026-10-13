# LiDire — Versão 81

## Alterações
- Remove o pequeno botão roxo sobreposto à foto do perfil.
- Inclui ajuste de zoom e posição para enquadrar a foto no círculo antes de salvar.
- Substitui o campo de idade no formulário de perfil por data de nascimento.
- Persiste a data de nascimento na tabela `profiles` (migração aditiva `birth_date`) e exibe uma saudação de aniversário na tela inicial no dia correspondente.
- Adiciona lupa na barra superior entre a foto do perfil e a seta de voltar; pesquisa as principais áreas/funções da LiDire.
- Melhora a exportação de dados: rótulos em português, datas em formato brasileiro e logo oficial no relatório imprimível/PDF.

## Testes realizados
- Verificação sintática de `app.js` e `index.js` com `node --check`.
- Integridade do ZIP verificada após empacotamento.

## Antes de publicar
- Faça backup do código e do banco D1.
- Faça deploy em ambiente de teste primeiro.
- Teste salvar/editar perfil e data de nascimento, enquadrar foto em diferentes aparelhos, pesquisa global, geração/ impressão do relatório e presença dos registros dos módulos.
- A geração de aniversário depende de a data de nascimento estar preenchida e salva.
- A exportação não deve incluir dados de outros membros da família, credenciais ou tokens.
