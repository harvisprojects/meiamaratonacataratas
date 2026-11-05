# Meia Maratona Internacional das 3 Fronteiras

Plataforma própria de inscrições da prova: site do evento, inscrição, pagamento por gateway, área do atleta e painel da organização.

## Estado atual

Protótipo navegável em [`prototipo/index.html`](prototipo/index.html). É um arquivo HTML único, sem servidor: abra no navegador.

- **Landing page:** data, percursos (21 km e 10,5 km), preços, retirada de kit, regulamento e dúvidas.
- **Inscrição:** percurso, categoria, dados do atleta (CPF para brasileiros, documento do país para estrangeiros), envio de documento e aceite dos termos.
- **Checkout do gateway:** tela simulada. No sistema real ela é do Mercado Pago (Checkout Pro) ou da Stripe.
- **Área do atleta:** número de peito, QR code para retirada do kit, status do documento e do pagamento, cancelamento em até 7 dias.
- **Painel da organização** (link "Organização" no rodapé): visão geral, inscritos, documentos, financeiro, contestações (chargeback) e entrega de kits.

Os dados são de exemplo, baseados na edição 2026, e ficam só no navegador (localStorage). Nenhum pagamento é real.

Para testar o cartão: `4242 4242 4242 4242` aprova e `4000 0000 0000 0002` é recusado.

## Próximo passo

Construir o sistema real seguindo o [plano](PLANO.md).
