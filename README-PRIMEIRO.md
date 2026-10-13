# LiDire — primeiro

Versão baseada no F2.1-main, com o bloco **Anotações** tornado funcional.

## O que foi implementado
- Criar anotação
- Editar anotação
- Excluir anotação
- Favoritar/desfavoritar
- Categoria
- Tags
- Busca por texto
- Filtro por categoria
- Filtro de favoritos
- Persistência por usuário no Cloudflare D1
- API `/api/notes` com GET/POST/PUT/DELETE
- Tabela `notes` e índices

A API também cria a tabela automaticamente na primeira utilização, para evitar depender de uma execução manual de SQL durante o primeiro deploy.

## Google Maps no Cloudflare

Para ativar o cálculo de rotas, cadastre `GOOGLE_MAPS_API_KEY` como **Secret** nas configurações do Worker Cloudflare. Consulte `CONFIGURACAO-GOOGLE-MAPS-CLOUDFLARE.md` para o passo a passo. A chave não deve ser inserida nos arquivos JavaScript do navegador nem no `wrangler.toml`.
