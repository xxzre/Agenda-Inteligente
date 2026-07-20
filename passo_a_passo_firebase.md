# Guia Passo a Passo: Configuração do Firebase no Agenda Inteligente

Este guia ensina como criar uma conta gratuita no Firebase da Google e obter as chaves de acesso para conectar o **Agenda Inteligente** ao banco de dados em nuvem.

---

## 1. Criar um Projeto no Firebase

1. Acesse o console do Firebase: [https://console.firebase.google.com/](https://console.firebase.google.com/)
2. Faça login com a sua conta Google.
3. Clique em **"Adicionar projeto"** (ou **"Criar um projeto"**).
4. Digite o nome do projeto (ex: `Agenda-Inteligente`).
5. (Opcional) Desative o *Google Analytics* para este projeto e clique em **Criar projeto**.
6. Aguarde alguns segundos e clique em **Continuar**.

---

## 2. Ativar a Autenticação (E-mail e Senha)

1. No menu lateral esquerdo do Firebase Console, clique em **Criação** > **Authentication**.
2. Clique no botão **Começar**.
3. Na aba **Provedores de login**, selecione **E-mail/senha**.
4. Ative a primeira chave de seleção (**E-mail/senha**).
5. Clique em **Salvar**.

---

## 3. Criar o Banco de Dados (Cloud Firestore)

1. No menu lateral esquerdo, clique em **Criação** > **Firestore Database**.
2. Clique em **Criar banco de dados**.
3. Escolha a localização do banco de dados (padrão `southamerica-east1` em São Paulo, ou a localização padrão sugerida) e clique em **Avançar**.
4. Em Regras de segurança, selecione **Iniciar no modo de teste** (para desenvolvimento rápido) e clique em **Criar**.
5. Na aba **Regras** do Firestore Database, insira a seguinte regra simples para segurança total por usuário:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Regra para permitir que qualquer usuário autenticado leia e escreva dados
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```
6. Clique em **Publicar**.

---

## 4. Registrar a Aplicação Web e Pegar as Chaves `firebaseConfig`

1. Na página inicial do seu projeto (clique no ícone da engrenagem ⚙️ > **Configurações do projeto**).
2. Na aba **Geral**, role até a seção *"Seus aplicativos"* e clique no ícone Web `</>`.
3. Digite o apelido do app (ex: `Agenda Web`) e clique em **Registrar app**.
4. O Firebase exibirá um código contendo o objeto `const firebaseConfig = { ... }`.
5. Copie o trecho das chaves:

```javascript
{
  apiKey: "AIzaSy...",
  authDomain: "agenda-inteligente.firebaseapp.com",
  projectId: "agenda-inteligente",
  storageBucket: "agenda-inteligente.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef..."
}
```

---

## 5. Inserir as Chaves no Agenda Inteligente

1. Abra o arquivo `index.html` no seu navegador.
2. Clique no botão **⚙️ Configurar Firebase** no topo da página.
3. Cole os valores das chaves ou o objeto `firebaseConfig` completo no campo e clique em **Salvar Conexão**.
4. Pronto! A tela de **Login / Cadastro** aparecerá automaticamente e todos os dados serão sincronizados na nuvem!
