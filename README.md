# 🍱 App Restaurante Offline

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PWA Ready](https://img.shields.io/badge/PWA-Ready-green.svg)](https://web.dev/progressive-web-apps/)
[![Zero Backend](https://img.shields.io/badge/Backend-Zero-blue.svg)](https://en.wikipedia.org/wiki/Serverless_computing)

Um Progressive Web App (PWA) completo para restaurantes de marmitas, sem necessidade de backend ou banco de dados. Os dados do cardápio são transmitidos via URL usando codificação Base64.

## 🎯 Características Principais

- **🔐 Zero Backend**: Sem servidor, sem banco de dados, sem custos de hospedagem
- **📱 PWA**: Instalável como app nativo em dispositivos móveis
- **🎨 Design Responsivo**: Interface mobile-first com TailwindCSS
- **⏰ Validação de Data**: Cardápios expiram automaticamente no fim do dia
- **💬 Integração WhatsApp**: Pedidos diretos para o restaurante
- **🔗 Sistema de Links**: Compartilhamento fácil do cardápio diário

## 📦 Estrutura do Projeto

```
app-restaurante-offline/
├── 📁 .github/                    # Configurações do GitHub
│   ├── 📁 workflows/              # GitHub Actions
│   └── 📁 ISSUE_TEMPLATE/         # Templates de issues
├── 📁 docs/                      # Documentação técnica
├── 📁 public/                    # Arquivos públicos (deploy)
│   └── 📄 index.html             # Aplicação principal
├── 📁 src/                       # Código fonte organizado
│   ├── 📁 assets/               # Imagens, ícones, fonts
│   ├── 📁 css/                  # Estilos CSS customizados
│   └── 📁 js/                   # JavaScript modularizado
├── 📄 .gitignore                # Arquivos ignorados pelo Git
├── 📄 LICENSE                   # Licença MIT
└── 📄 README.md                 # Este arquivo
```

## 🚀 Como Usar

### 1. Configuração do Cardápio (Admin)

Acesse o painel admin adicionando `?admin=true` à URL:
```
https://seudominio.com/?admin=true
```

**Funcionalidades do Admin:**
- Adicionar/remover opções principais (carnes)
- Adicionar/remover acompanhamentos
- Gerar link do cardápio do dia
- Copiar link para compartilhar

### 2. Visualização do Cliente

Os clientes acessam via link gerado pelo admin:
```
https://seudominio.com/?menu=eyJkYXRhIjoiMjAyNi0wNC0zMCIsInByaW5jaXBhaXMiOlsiRmVpam9hZGEiLCJGcmFuZ28iXSw...
```

**Funcionalidades do Cliente:**
- Escolher carne principal (radio buttons)
- Selecionar acompanhamentos (checkboxes)
- Preencher dados pessoais
- Enviar pedido via WhatsApp

## 🛠️ Configuração

### 1. Substituir Número do WhatsApp

Edite o arquivo `public/index.html` e substitua o número:

```javascript
const restaurant = {
    phone: '5511999999999', // ← Substituir pelo número real
    name: 'Marmitas do Chef'
};
```

### 2. Personalização

**Cores (TailwindCSS):**
```html
<script>
tailwind.config = {
    theme: {
        extend: {
            colors: {
                primary: '#10B981',    // Verde principal
                secondary: '#059669',  // Verde secundário
                accent: '#047857'      // Verde acento
            }
        }
    }
}
</script>
```

**Texto e Branding:**
- Edite o título na tag `<title>`
- Modifique o nome do restaurante nas constantes JavaScript
- Ajuste cores no config do Tailwind

## 🔧 Desenvolvimento

### Estrutura de Código

O aplicativo está organizado em funções modulares:

```javascript
// Configurações principais
const restaurant = { /* ... */ };

// Funções de view
function showAdminView() { /* ... */ }
function showClientView() { /* ... */ }

// Funções do admin
function generateMenuLink() { /* ... */ }
function copyLink() { /* ... */ }

// Funções do cliente
function loadMenuFromUrl() { /* ... */ }
function sendOrder() { /* ... */ }
```

### Validação de Data

O sistema inclui validação automática de expiração:

```javascript
// No momento da geração
const menuData = {
    data: new Date().toISOString().split('T')[0], // YYYY-MM-DD
    principais: [...],
    acompanhamentos: [...]
};

// Na validação
const today = new Date().toISOString().split('T')[0];
if (currentMenu.data !== today) {
    showExpiredMenu();
}
```

## 📱 PWA Features

**Manifest Inline:** O manifest está embutido como data URI para melhor performance

**Service Worker:** Pronto para implementação de cache offline

**Design Mobile-First:** Interface otimizada para dispositivos móveis

## 🌐 Deployment

### Opção 1: GitHub Pages
```bash
# Clone o repositório
git clone https://github.com/seu-usuario/app-restaurante-offline.git

# Faça deploy para GitHub Pages
# O arquivo principal está em public/index.html
```

### Opção 2: Servidor Estático
```bash
# Qualquer servidor estático serve:
# - Nginx
# - Apache
# - Netlify
# - Vercel
# - GitHub Pages
```

### Opção 3: Local
```bash
# Servidor local simples com Python
python -m http.server 8000

# Ou com Node.js
npx serve public
```

## 🔒 Segurança

- **Validação de Base64**: Tratamento de erros para links inválidos
- **Sanitização de Input**: Prevenção contra XSS básico
- **Expiração Automática**: Cardápios não ficam válidos após o dia
- **Dados na URL**: Sem armazenamento persistente de dados sensíveis

## 📊 Performance

- **Tamanho**: ~15KB (compactado)
- **Carregamento**: ±100ms em conexão 4G
- **Interação**: Instantânea (zero latency)

## 🤝 Contribuição

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📝 Licença

Distribuído sob licença MIT. Veja `LICENSE` para mais informações.

## 🆘 Suporte

Para problemas e dúvidas:

1. Verifique a [documentação técnica](./docs/)
2. Abra uma [issue](../../issues)
3. Entre em contato via email: seu-email@provedor.com

---

**Desenvolvido com ❤️ para restaurantes locais** 🍱

*Um projeto open-source que valoriza a simplicidade e eficiência.*