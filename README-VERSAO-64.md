# LiDire — Versão 64

## Alteração desta versão
- Adicionado preenchimento automático de endereços com sugestões enquanto o usuário digita na tela **Clima e Rotas**, nos campos de clima, origem, destino e endereço de lugares frequentes.
- As sugestões são consultadas no backend Cloudflare Worker pela API Places (New), sem expor a chave no navegador.
- A busca começa a partir de 3 caracteres, usa pequeno atraso para evitar chamadas excessivas e permite selecionar a sugestão para preencher o campo.

## Configuração necessária
A chave `GOOGLE_MAPS_API_KEY` já usada pelo Worker precisa ter a **Places API (New)** habilitada no mesmo projeto Google Cloud e faturamento configurado. A chave permanece como Secret no Cloudflare; não a inclua nos arquivos do front-end. Se a Places API não estiver habilitada, as sugestões não serão exibidas, mas o preenchimento manual continua disponível.
\n\n## Versão 64 — rotas e Waze\n- Corrigida a conversão de origem e destino para links externos do Google Maps.\n- Adicionado botão para abrir o destino no Waze usando Waze Deep Links.\n