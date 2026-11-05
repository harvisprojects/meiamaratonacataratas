# Meia Maratona Internacional das 3 Fronteiras

Plataforma própria de inscrições da prova: site do evento, inscrição, pagamento por gateway, área do atleta e painel da organização.

## Estado atual

Protótipo navegável em [`prototipo/index.html`](prototipo/index.html). É um arquivo HTML único, sem servidor: abra no navegador.

- **Landing page:** página única e simples: hero com mapa do percurso, as duas distâncias (21K e 10K), kits, informações práticas e dúvidas.
- **Kit Fronteira Pro:** um kit único, incluso em toda inscrição (camiseta, kit compressão, meia de compressão, manguito, cap, botton e squeeze), com destaque na landing page junto com a área VIP, a retirada sem fila e a volta garantida para Foz.
- **Inscrição:** distância, dados do atleta (CPF para brasileiros, documento do país para estrangeiros) e aceite do regulamento. Sem categorias especiais: o produto é o mesmo para todos.
- **Checkout do gateway:** tela simulada. No sistema real ela é do Mercado Pago (Checkout Pro) ou da Stripe.
- **Área do atleta:** número de peito, QR code para retirada do kit, status do documento e do pagamento, cancelamento em até 7 dias.
- **Painel da organização** (link "Organização" no rodapé): cinco telas. Resumo, Inscritos (com ficha do atleta e reembolso), Pagamentos (financeiro e contestações), Entrega de kits e Ajustes (preços, conta do administrador, organização e equipe).

Os dados são de exemplo, baseados na edição 2027, e ficam só no navegador (localStorage). Nenhum pagamento é real.

## Modo de teste

Tudo vem preenchido com dados fictícios para validar os fluxos rápido:

- **Barra "Modo de teste"** no topo de todas as páginas, com atalhos "Entrar como atleta" e "Entrar como organização".
- **Inscrição** já abre preenchida com um atleta fictício (CPF válido gerado na hora). "Novos dados fictícios" gera outro; "Limpar" esvazia.
- **Checkout** já vem com o cartão de teste `4242 4242 4242 4242` (aprovado). O link "Testar cartão recusado" troca para `4000 0000 0000 0002`. No Pix, o botão "Simular Pix recebido" confirma o pagamento.
- **Área do atleta** e **painel da organização** abrem com e-mails fictícios já preenchidos (`@exemplo.com`).

## Próximo passo

Construir o sistema real seguindo o [plano](PLANO.md).
