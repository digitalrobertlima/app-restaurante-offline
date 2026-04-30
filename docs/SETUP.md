# 🚀 Guia de Setup e Deploy

## 📋 Pré-requisitos

- **Git**: Para versionamento do código
- **GitHub CLI (opcional)**: Para gerenciamento do repositório
- **Servidor estático**: Qualquer servidor web (Nginx, Apache, etc.)

## 🛠️ Setup Local

### 1. Clonar o Repositório

```bash
git clone https://github.com/digitalrobertlima/app-restaurante-offline.git
cd app-restaurante-offline
```

### 2. Servidor Local de Desenvolvimento

**Opção A: Python**
```bash
python -m http.server 8000
# Acesse: http://localhost:8000/public
```

**Opção B: Node.js**
```bash
npx serve public
# Acesse: http://localhost:3000
```

**Opção C: PHP**
```bash
php -S localhost:8000 -t public
# Acesse: http://localhost:8000
```

## 🌐 Deploy em Produção

### 1. GitHub Pages (Recomendado)

O repositório já está configurado com GitHub Actions para deploy automático.

**Passos:**
1. Vá em Settings → Pages
2. Selecione "GitHub Actions" como source
3. Faça push para a branch `main`

**URL do Deploy:**
```
https://digitalrobertlima.github.io/app-restaurante-offline/public/
```

### 2. Netlify

**Deploy Manual:**
1. Faça upload da pasta `public` no netlify.com
2. Ou conecte o repositório GitHub

**Deploy via CLI:**
```bash
npm install -g netlify-cli
netlify deploy --dir=public --prod
```

### 3. Vercel

```bash
npm install -g vercel
vercel --prod public
```

### 4. Servidor Próprio

**Nginx Config:**
```nginx
server {
    listen 80;
    server_name seusite.com;
    root /caminho/para/app-restaurante-offline/public;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

## ⚙️ Configuração do App

### 1. Número do WhatsApp

Edite `public/index.html` e substitua:

```javascript
const restaurant = {
    phone: '5511999999999', // ← Número real com DDD e código do país
    name: 'Marmitas do Chef'
};
```

### 2. Personalização de Branding

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

**Texto:**
- Modifique a tag `<title>`
- Ajuste o nome do restaurante nas constantes JavaScript

## 🔧 Desenvolvimento

### Estrutura de Arquivos

```
app-restaurante-offline/
├── public/
│   └── index.html              # Aplicação principal
├── src/                       # Para futura modularização
│   ├── assets/               # Imagens, ícones
│   ├── css/                  # Estilos adicionais
│   └── js/                   # JavaScript modular
├── docs/                     # Documentação
└── .github/                  # GitHub Actions e templates
```

### Adicionando Novas Funcionalidades

1. **Modularize o código** em `src/js/`
2. **Adicione estilos** em `src/css/`
3. **Atualize a documentação**

## 📱 Testes

### Testes Manuais

1. **Painel Admin**: `?admin=true`
   - Adicione itens ao cardápio
   - Gere link
   - Copie link

2. **Visão Cliente**: Use o link gerado
   - Monte pedidos
   - Teste envio WhatsApp
   - Valide expiração de data

### Testes Automáticos (Futuro)

Planejado para implementar:
- Jest para testes unitários
- Cypress para testes E2E
- GitHub Actions CI/CD

## 🔒 Segurança em Produção

### Boas Práticas

1. **HTTPS**: Sempre use HTTPS em produção
2. **Validação**: O app já valida data e Base64
3. **Sanitização**: Inputs são validados
4. **CORS**: Configure corretamente se usar APIs

### Monitoramento

- **Console errors**: Verifique erros no browser
- **Performance**: Use Lighthouse para otimização
- **Analytics**: Considere adicionar Google Analytics

## 🚨 Troubleshooting

### Problemas Comuns

**Link não funciona:**
- Verifique se o Base64 está correto
- Confirme a data no objeto JSON

**WhatsApp não abre:**
- Verifique o número formatado corretamente
- Teste no dispositivo móvel

**CSS não carrega:**
- Verifique conexão com internet
- Confirme CDN do Tailwind

### Logs de Debug

Adicione no console para debug:
```javascript
console.log('Menu data:', currentMenu);
console.log('URL params:', new URLSearchParams(window.location.search));
```

## 📞 Suporte

1. **Documentação**: Verifique os arquivos em `docs/`
2. **Issues**: Abra uma issue no GitHub
3. **Community**: Participe das discussões

---

**⭐ Dica**: Para melhor performance, considere usar um CDN para assets estáticos e implementar service worker para cache offline.

**Happy Coding!** 🚀