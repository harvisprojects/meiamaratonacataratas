# Plano do sistema real

Três fases, de 7 a 9 semanas no total, para ficar pronto antes da abertura das inscrições.

## 1. Arquitetura

Site, inscrição, área do atleta e painel ficam num único projeto, com um único banco de dados. Só o checkout fica no gateway.

```
Atleta → Landing → Inscrição → [Checkout do gateway] → Área do atleta
                                       │
                         aviso automático (webhook)
                                       ↓
                           Banco de dados ← Painel da organização
```

## 2. Ferramentas e custo mensal

| Para quê | Ferramenta | Custo aproximado |
|---|---|---|
| Site + painel | Next.js na Vercel (plano Pro, exigido para uso comercial) | US$ 20/mês |
| Banco, login por link no e-mail, arquivos dos documentos | Supabase (plano Pro) | US$ 25/mês |
| E-mails automáticos (~12 mil por mês) | Resend | US$ 20/mês |
| Pagamento | Mercado Pago (Checkout Pro) ou Stripe | taxa por venda |
| Domínio | registro.br | ~R$ 40/ano |

Total fixo: cerca de R$ 350/mês durante o período de inscrições.

**Decisão em aberto:** o gateway precisa aceitar cartões emitidos no Paraguai e na Argentina. A Stripe aceita, mas libera Pix no Brasil só por convite. O Mercado Pago tem Pix; confirmar com eles os cartões estrangeiros.

## 3. Fluxo do pagamento

1. O atleta preenche a inscrição. O sistema cria um pedido "aguardando pagamento" e segura a vaga por 30 minutos.
2. O atleta paga no checkout do gateway.
3. O gateway avisa o sistema por webhook. Só esse aviso confirma o pagamento; o retorno do navegador nunca conta.
4. O sistema confirma a inscrição, gera o número de peito e envia o e-mail com o QR code.
5. Se o pagamento não cair em 30 minutos, a vaga volta para a venda.

O webhook deve ser idempotente: o mesmo aviso recebido duas vezes não confirma a inscrição duas vezes.

## 4. Fases

**Fase 0: preparação (1 semana)**
- Conta PJ no gateway e no Supabase, domínio e e-mail do domínio.
- Regulamento, termo de responsabilidade e política de privacidade (LGPD) revisados por advogado.
- Preços, limite de vagas, taxa de serviço e datas definidos.

**Fase 1: vender (3 a 4 semanas)**
- Landing, inscrição, checkout, webhook, e-mails e Área do atleta.
- Testes com pagamentos reais de R$ 1. Ao final, as inscrições podem abrir.

**Fase 2: controlar (2 a 3 semanas)**
- Painel: inscritos, ficha do atleta, aprovação de documentos, reembolso via gateway, financeiro e exportação para planilha.
- Login individual da equipe, com permissões.

**Fase 3: dia da prova (1 a 2 semanas, até um mês antes do evento)**
- Entrega de kits com leitura do QR code pela câmera do celular.
- Tela de contestações com as provas reunidas.
- Versão em espanhol e exportação da lista para a cronometragem.

## 5. Responsáveis

- Construção: organização + Claude Code, seguindo o protótipo.
- Revisão de segurança e pagamento: dev experiente, de 10 a 20 horas, antes de abrir.
- Termos, regulamento e LGPD: advogado.
- Nota fiscal (NFS-e) sobre a taxa de serviço: contador.

## 6. Riscos

- Pico na abertura: o limite de vagas é controlado no banco, para nunca vender acima do limite.
- Documentos dos atletas: armazenamento privado, apagados depois do evento.
- Backup diário do banco.
- Contestações: guardar aceite com data e IP; cancelamento fácil na Área do atleta.

## 7. Checklist antes de abrir as inscrições

- [ ] 5 pagamentos reais testados: Pix, cartão à vista, parcelado, estrangeiro e um reembolso.
- [ ] Pagamento recusado e Pix expirado não geram inscrição.
- [ ] E-mails chegam na caixa de entrada, não no spam.
- [ ] Código revisado pelo dev.
- [ ] Termos e política de privacidade publicados.
