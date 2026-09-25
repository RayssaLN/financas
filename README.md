# 💜 Finanças

App web de finanças pessoais e de casal, criado para substituir as minhas planilhas de controle financeiro e deixar tudo num lugar só.

🔗 **Acesse:** https://rayssaln.github.io/financas/

---

## ✨ Funcionalidades

- **Gastos do mês:** orçamento previsto x real por categoria e renda separada por fonte.
- **Cartão de crédito:** compras parceladas, contas no cartão, estornos e conferência da fatura com o banco.
- **Caixinhas:** metas com aportes, resgates e rendimentos, incluindo o acompanhamento "vale a pena?" de assinaturas.
- **Reserva de emergência:** meta em meses de custo de vida e evolução mês a mês.
- **Investimentos:** ativos, preço médio e compras de ações, FIIs e cripto.
- **Rendimentos:** proventos (dividendos, JCP e rendimentos de FIIs) e rendimento das caixinhas.
- **Análise da carteira:** diversificação por classe, alocação ideal, meta anual e um simulador de aporte ("vou investir R$ X, onde aplico?").
- **Casal 💑:** cada pessoa tem o próprio login, um pode ver a tela do outro, e as caixinhas do casal e o patrimônio somado ficam compartilhados.
- **Extras:** 6 paletas de cores, modo escuro, backup e restauração em JSON, e pode ser instalado no celular.

## 🛠️ Tecnologias

- HTML, CSS e JavaScript puro, sem framework
- [Firebase Authentication](https://firebase.google.com/docs/auth) para o login com Google
- [Cloud Firestore](https://firebase.google.com/docs/firestore) como banco de dados em tempo real
- GitHub Pages para a hospedagem
- Gráficos em SVG feitos à mão

## 📁 Estrutura

```
index.html          → o app inteiro (telas, estilos e lógica)
firebase-config.js  → configuração pública do projeto Firebase
firestore.rules     → regras de segurança do banco
manifest.json       → configuração para instalar no celular
icon.svg            → ícone do app
```

## 🔒 Segurança

Os dados ficam no Firestore, em `users/{uid}/...`, e cada pessoa só altera os próprios dados. As regras em `firestore.rules` permitem que o par vinculado no casal apenas **leia** a parte pessoal do outro, e que os dois editem juntos a área do casal (`casais/{id}/...`).

Nenhum dado financeiro fica neste repositório.

---

Feito por **Rayssa** 💜
