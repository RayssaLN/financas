# 💜 Finanças

App web de finanças pessoais e de casal, criado para substituir planilhas de controle financeiro e deixar tudo em um só lugar.

🔗 **Acesse:** https://rayssaln.github.io/financas/

## ✨ Funcionalidades

### Dia a dia
- **Início:** resumo do mês (quanto entrou, saiu e sobrou), fatura do mês escolhido, gráfico do ano e para onde foi o dinheiro.
- **Lançamento rápido:** botão **+** para lançar um gasto em poucos toques, com categoria sugerida automaticamente pelo nome e opção de conta recorrente.
- **Gastos do mês:** orçamento previsto x real por categoria e renda separada por fonte (renda, saldo anterior, renda extra, benefício, transferência).
- **Importar extrato:** lê arquivos CSV, OFX e o PDF da fatura do Nubank, identifica a categoria de cada compra e aprende com as correções.
- **Cartão de crédito:**
  - fatura por mês, respeitando o dia de fechamento e de vencimento de cada cartão, com conferência do valor do banco;
  - compras parceladas, com opção de antecipar, juntar ou pular parcelas;
  - registro do pagamento da fatura (quanto saiu da caixinha e quanto de outro jeito), que já marca as parcelas como pagas;
  - contas fixas no cartão, com ou sem dinheiro guardado antes;
  - estornos e resumo de **para onde foi o cartão** por categoria.
- **Empréstimos:** o que você pegou emprestado e o que emprestou para alguém, com parcelas, pagamentos parciais e opção sem data. Tudo entra automaticamente nos gastos e na renda do mês.
- **Meli+:** acompanha a caixinha do Mercado Pago com a assinatura, atualizando o saldo e mostrando se a mensalidade está valendo a pena.

### Guardar
- **Caixinhas:** metas com aportes, resgates e rendimentos.
- **Caixinha do cartão:** dinheiro separado para pagar a fatura, com o checklist mensal "Guardei".
- **Reserva de emergência:** meta em meses de custo de vida e evolução mês a mês.

### Investir
- **Investimentos:** ativos, preço médio e compras de ações, FIIs e cripto.
- **Rendimentos:** proventos (dividendos, JCP e rendimentos de FIIs) e rendimento das caixinhas.
- **Análise da carteira:** diversificação por classe, alocação ideal, meta anual e um simulador de aporte ("vou investir R$ X, onde aplico?").
- **Patrimônio:** imóveis, veículos e outros bens. Para veículos, o valor vem da tabela FIPE e se atualiza sozinho todo mês.

### Casal 💑
Cada pessoa tem o próprio login com Google e pode ver as telas da outra, sem poder alterar. As caixinhas do casal ficam compartilhadas e cada um pode colocar a própria foto de perfil.

### Extras
Paletas de cores, modo escuro, menu personalizável, backup e restauração em JSON. O app também pode ser instalado no celular (PWA).

## 🛠️ Tecnologias

- HTML, CSS e JavaScript puro, sem framework
- [Firebase Authentication](https://firebase.google.com/docs/auth) para o login com Google
- [Cloud Firestore](https://firebase.google.com/docs/firestore) como banco de dados em tempo real
- [API FIPE](https://deividfortuna.github.io/fipe/) para o valor dos veículos
- [PDF.js](https://mozilla.github.io/pdf.js/) para ler a fatura em PDF
- GitHub Pages para a hospedagem
- Gráficos em SVG feitos à mão

## 📁 Estrutura

```
icons/              → ícones do app (navegador, celular e iPhone)
index.html          → o app inteiro (telas, estilos e lógica)
manifest.json       → configuração para instalar no celular
firebase-config.js  → configuração pública do projeto Firebase
firestore.rules     → regras de segurança do banco
```

## 🔒 Segurança

Os dados ficam no Firestore, em `users/{uid}/...`, e cada pessoa só altera os próprios dados. As regras em `firestore.rules` permitem que o par vinculado no casal apenas leia a parte pessoal do outro, e que os dois editem juntos a área do casal (`casais/{id}/...`).

A chave em `firebase-config.js` é pública por natureza: ela só identifica o projeto. Quem protege os dados são o login e as regras do Firestore.

Nenhum dado financeiro fica neste repositório.

---

Feito por Rayssa e Kelvyn 💜
