# LiDire — Versão 73

## Exportação pessoal
- O download passa a gerar um relatório HTML legível, com títulos e campos em português.
- Removidos o ID da conta e identificadores internos dos registros exibidos.
- Incluídos avisos claros quando categorias não puderem ser exportadas.
- Mantida a filtragem de credenciais, tokens e sessões.

## Listas de compras
- Cada lista agora apresenta ações visíveis para editar seu nome e excluí-la.
- Exclusão exige confirmação.
- A seleção da lista permanece separada dos botões de edição e exclusão.

## Validação
- Sintaxe de `app.js` e `index.js` validada com `node --check`.
- A integração com o banco D1 e a interface devem ser testadas após publicação.
