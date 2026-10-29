MANDACARU GAMES PS3 — Landing page + checkout transparente HyperCash (Pix e cartão dentro do site)

ESTRUTURA
  index.html        landing page do PS3 (botões levam ao checkout)
  checkout.html     checkout completo: frete, dados, endereço e pagamento (Pix / cartão)
  api/checkout.js   função do servidor (Vercel): cria a cobrança, config e status
  css/ js/          estilos (css/ps3.css = tema preto/laranja) e scripts (js/config.js = textos/preço de vitrine; js/pedido.js = lógica do checkout)
  images/           logo, favicon e imagem reserva

VARIÁVEIS NA VERCEL (Settings > Environment Variables)
  HYPER_SECRET_KEY       chave SECRETA da HyperCash (painel HyperCash > API / Integrações)
  HYPER_PUBLIC_KEY       chave PÚBLICA da HyperCash (começa com pk_live_...)
  PRODUCT_PRICE_CENTS    26990   (R$ 269,90 em centavos)
  SEDEX_PRICE_CENTS      1290    (opcional)
  CARD_MAX_INSTALLMENTS  3       (opcional, máximo de parcelas no cartão)
  Depois de criar/alterar variáveis, faça Redeploy.

APAGAR (não são mais usadas)
  PAGOU_API_KEY, PAGOU_PUBLIC_KEY, PAGOU_ENV

TESTES
  A HyperCash só tem ambiente de PRODUÇÃO (não existe sandbox). Para testar sem gastar:
  coloque PRODUCT_PRICE_CENTS=500 (R$ 5,00), faça Redeploy, pague um Pix de verdade e confira
  no painel da HyperCash. Depois volte o preço certo e faça Redeploy de novo.
  Se algo falhar, veja Vercel > seu projeto > Logs: a resposta de erro da HyperCash aparece lá
  (linhas "hyper_error ...").

IMPORTANTE
  - A chave secreta NUNCA vai no GitHub nem no navegador, só na Vercel.
  - O valor cobrado vem do servidor. Se mudar o preço, mude na Vercel E em js/config.js (que só exibe: campo "preco"; "precoAntigo" é o preço riscado, 0 = esconde).
  - O GitHub Pages NÃO serve: ele não roda a pasta api/. Use a Vercel.
  - Pedidos, endereços e status aparecem no painel da HyperCash.
