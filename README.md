# Ranking de Levantadas — Equipe Sucesso

## Como publicar no Firebase Hosting

### 1. Criar o projeto no Firebase
- Acesse https://console.firebase.google.com
- Clique em "Criar projeto" → dê um nome (ex: `ranking-sucesso`)
- Ative o **Firestore Database** (modo produção)
- Ative o **Firebase Hosting**

### 2. Editar o .firebaserc
Abra o arquivo `.firebaserc` e substitua `SEU-PROJECT-ID-AQUI` pelo ID do seu projeto Firebase.

### 3. Instalar Firebase CLI (só uma vez)
```bash
npm install -g firebase-tools
firebase login
```

### 4. Fazer o deploy
```bash
firebase deploy
```

Pronto! O Firebase Hosting injeta as credenciais automaticamente via `/__/firebase/init.json`.  
**Nenhuma credencial fica exposta no código.**

### Regras do Firestore recomendadas
No console do Firebase → Firestore → Regras:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /analistas/{id} {
      allow read, write: if true;
    }
    match /checkpoints/{id} {
      allow read, write: if true;
    }
  }
}
```

### Estrutura de coleções no Firestore
- `analistas/` → lista de CSs (campo: `nome`)
- `checkpoints/` → registros de evolução (campos: `label`, `mes`, `dados`, `criadoEm`)
