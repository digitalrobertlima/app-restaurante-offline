# 🏗️ Arquitetura do Sistema

## 📋 Visão Geral

O App Restaurante Offline é um Progressive Web App (PWA) construído com uma arquitetura **zero-backend**, onde todos os dados são transmitidos via URL usando codificação Base64.

## 🎯 Princípios de Design

### 1. **Simplicidade**
- Single HTML File
- Zero Dependencies (exceto TailwindCDN)
- Sem Build Process

### 2. **Portabilidade**
- Funciona em qualquer servidor estático
- Sem requisitos de banco de dados
- Fácil deploy em múltiplas plataformas

### 3. **Segurança**
- Validação de data automática
- Sanitização de inputs
- Dados transitórios (não persistentes)

## 🔧 Stack Tecnológica

| Camada | Tecnologia | Propósito |
|--------|------------|-----------|
| **Frontend** | HTML5 | Estrutura semântica |
| **Estilos** | TailwindCSS | Design system utilitário |
| **Lógica** | Vanilla JavaScript | Funcionalidades do app |
| **PWA** | Web App Manifest | Capacidades nativas |
| **Data Transfer** | Base64 + URL Params | Transmissão de dados |

## 📊 Fluxo de Dados

### 1. Geração do Cardápio (Admin)
```
Form Input → JavaScript Object → JSON String → Base64 → URL Parameter
```

### 2. Consumo do Cardápio (Cliente)
```
URL Parameter → Base64 → JSON String → JavaScript Object → UI Render
```

### 3. Validação de Data
```javascript
// No generation
{ data: "2026-04-30", itens: [...] }

// Na validação
currentMenu.data === new Date().toISOString().split('T')[0]
```

## 🏛️ Estrutura de Código

### Organização Modular
```javascript
// Configurações globais
const restaurant = { /* ... */ };

// Views
function showAdminView() { /* ... */ }
function showClientView() { /* ... */ }

// Admin Functions
function generateMenuLink() { /* ... */ }

// Client Functions  
function loadMenuFromUrl() { /* ... */ }
function sendOrder() { /* ... */ }

// Utilities
function showToast() { /* ... */ }
function validateMenu() { /* ... */ }
```

### Sistema de Views
O app possui três estados principais:

1. **Admin View** (`?admin=true`)
2. **Client View** (`?menu=...`)
3. **Loading/Error View**

## 🔐 Segurança

### Validações Implementadas

1. **Base64 Validation**
```javascript
try {
    const menuJson = atob(menuBase64);
    currentMenu = JSON.parse(menuJson);
} catch (error) {
    showError('Link inválido');
}
```

2. **Date Validation**
```javascript
const today = new Date().toISOString().split('T')[0];
if (currentMenu.data !== today) {
    showExpiredMenu();
}
```

3. **Input Sanitization**
- Trim de espaços em branco
- Filtro de valores vazios
- Validação de required fields

## 📱 PWA Features

### Manifest Inline
```html
<link rel="manifest" href="data:application/json;base64,ewogICAg...">
```

### Service Worker Ready
A estrutura está preparada para adição de service worker para cache offline.

### Mobile Optimization
- Viewport configurado
- Touch-friendly buttons
- Responsive design

## 🚀 Performance Considerations

### Optimizations
- **Minimal CSS**: Tailwind purge ready
- **No External JS**: Zero dependencies
- **Efficient DOM**: Virtual DOM não necessário

### Loading Strategy
- Critical CSS inlined
- Lazy loading ready
- Progressive enhancement

## 🔮 Extensibilidade

### Possíveis Melhorias
1. **Service Worker**: Cache offline de assets
2. **LocalStorage**: Persistência de preferências
3. **IndexedDB**: Histórico de pedidos local
4. **Push Notifications**: Alertas de novo cardápio

### Modularização Futura
O código está organizado para fácil extração em módulos:
- `admin.module.js`
- `client.module.js` 
- `utils.module.js`
- `validation.module.js`

## 📊 Data Schema

### Menu Object
```json
{
  "data": "2026-04-30",
  "principais": ["Feijoada", "Frango", "Carne"],
  "acompanhamentos": ["Arroz", "Feijão", "Farofa", "Salada"]
}
```

### Order Object
```json
{
  "cliente": "João Silva",
  "endereco": "Rua A, 123",
  "principal": "Feijoada",
  "acompanhamentos": ["Arroz", "Farofa"],
  "data": "30/04/2026"
}
```

## 🌐 Deployment Arch

### Static Hosting Ready
- GitHub Pages
- Netlify
- Vercel
- S3 + CloudFront
- Any web server

### No Server Requirements
- Zero API endpoints
- No database connections
- No server-side processing

---

**Arquitetura projetada para máxima simplicidade e eficiência** 🚀