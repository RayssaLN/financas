# Finanças da Rayssa: como publicar de graça

O site fica no **GitHub Pages** e os dados ficam no **Firebase**. Os dois são gratuitos para uso pessoal e não pedem cartão de crédito. Só você consegue ver os dados, porque o acesso é feito com login pela sua conta Google.

Leva uns 20 minutos, e você só precisa fazer isso uma vez.

---

## Parte 1: Firebase (onde ficam os dados)

1. Entre em **https://console.firebase.google.com** com a sua conta Google.
2. Clique em **Criar um projeto** e dê um nome, por exemplo `financas-rayssa`. Pode desativar o Google Analytics, porque ele não é necessário.
3. **Ligue o login com Google:**
   - No menu da esquerda, abra **Criação > Authentication > Vamos começar**.
   - Na aba **Método de login**, escolha **Google**, clique em **Ativar**, selecione o seu e-mail de suporte e salve.
4. **Crie o banco de dados:**
   - Abra **Criação > Firestore Database > Criar banco de dados**.
   - Escolha a localização **southamerica-east1 (São Paulo)**.
   - Escolha **Iniciar no modo de produção**.
5. **Cole as regras de segurança:**
   - Ainda no Firestore, abra a aba **Regras**.
   - Apague o que estiver lá, cole o conteúdo do arquivo `firestore.rules` e clique em **Publicar**.
   - Essas regras garantem que cada pessoa só consegue ler os próprios dados.
6. **Pegue a configuração do app:**
   - Clique na engrenagem ⚙️ > **Configurações do projeto**.
   - Em **Seus apps**, clique no ícone **</>** (Web), dê um apelido (`site`) e clique em **Registrar app**. Não precisa marcar o Firebase Hosting.
   - Vai aparecer um bloco `const firebaseConfig = { ... }`. Copie os valores de dentro dele para o arquivo **`firebase-config.js`**, substituindo os que começam com `COLE_AQUI` e `SEU-PROJETO`.

> Esses valores do `firebase-config.js` podem ficar públicos sem problema. O que protege os seus dados são as regras do passo 5 junto com o login.

---

## Parte 2: GitHub Pages (onde fica o site)

1. Crie uma conta em **https://github.com**, se ainda não tiver.
2. Clique em **New repository**, dê o nome `financas`, deixe como **Public** e crie.
3. Clique em **uploading an existing file** e arraste estes arquivos:
   `index.html`, `firebase-config.js` (já preenchido), `manifest.json`, `icon.svg`, `firestore.rules`, `.gitignore` e este `LEIA-ME.md`.
   ⚠️ **Não envie o arquivo de backup (`financas-backup-....json`).** Ele tem os seus dados financeiros, e o repositório é público.
4. Clique em **Commit changes**.
5. Vá em **Settings > Pages**. Em **Branch**, escolha `main` e a pasta `/ (root)`, e clique em **Save**.
6. Em 1 ou 2 minutos, o site vai estar em **`https://SEU-USUARIO.github.io/financas/`**.

## Parte 3: liberar o seu site no login do Google

1. No Firebase, abra **Authentication > Configurações > Domínios autorizados > Adicionar domínio**.
2. Digite **`SEU-USUARIO.github.io`**, sem `https://` e sem `/financas`.

## Parte 4: trazer os seus dados

1. Abra o seu site e clique em **Entrar com Google**.
2. No menu, clique em **Backup dos dados > Restaurar um backup**.
3. Escolha o arquivo **`financas-backup-2026-09-25.json`** e clique em **Importar**.

Pronto! A partir daí, tudo o que você lançar fica salvo no seu Firebase.

---

## Dicas

- **No celular:** abra o site no Chrome (Android) ou no Safari (iPhone) e use **Adicionar à tela inicial**. Ele passa a abrir como um aplicativo, com o ícone do R.
- **Backup:** de vez em quando, use **Backup dos dados > Baixar backup** e guarde o arquivo no Google Drive.
- **Mudanças no código:** para mudar o `index.html`, edite o arquivo no GitHub (ícone de lápis) e salve. O site se atualiza sozinho em cerca de 1 minuto.
- **Custo:** o plano gratuito do Firebase (Spark) tem uma cota muito maior do que um app pessoal usa. Se um dia a cota acabar, o Firebase para de responder até o dia seguinte. Ele **não cobra nada** sem você cadastrar um cartão.

## Como o código funciona (para estudar 🤓)

- Todo o app está no `index.html`: HTML, CSS e JavaScript puro, sem framework.
- O script do `<head>` faz o login e cria um "adaptador". Os dados ficam em `users/{seu id}/{coleção}/{documento}` no Firestore. As coleções são `orcamento`, `cartao`, `potes`, `config`, `cartaoinfo`, `proventos`, `historico` e `meliuz`.
- O estado fica no objeto `S`. Cada tela é uma função que devolve HTML (`vInicio`, `vGastos`, `vCartao`...), e a função `render()` redesenha a tela quando os dados mudam.
- Os gráficos são SVG feitos à mão, na função `barChart`.
