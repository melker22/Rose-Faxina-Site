# Rose Faxina — Site Institucional

Landing page estática da **Rose Faxina**, serviço de faxina e limpeza doméstica profissional em **Mineiros (GO)**. O site apresenta os serviços, diferenciais, fluxo de agendamento e canais de contato, com foco em conversão via **WhatsApp** e formulário de e-mail.

**Site em produção:** [rosefaxina.com.br](https://rosefaxina.com.br)

**Deploy automático:** push na `main` → FTP HostGator — veja [DEPLOY-AUTOMATICO.md](DEPLOY-AUTOMATICO.md)
[![GitHub](https://img.shields.io/badge/GitHub-melker22%2FRose--Faxina--Site-181717?logo=github)](https://github.com/melker22/Rose-Faxina-Site)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/pt-BR/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)](https://developer.mozilla.org/pt-BR/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript)

---

## Sobre o projeto

A Rose Faxina conecta clientes a profissionais de limpeza verificados. Este repositório contém o site de apresentação: uma **página única (single page)** com navegação por âncoras, design responsivo em tons de rosa e roxo, animações leves ao rolar a página e integração direta com WhatsApp e FormSubmit para contato.

**Público-alvo:** moradores de Mineiros e região que buscam agendar limpeza residencial de forma rápida e segura.

---

## Funcionalidades do site

| Recurso | Descrição |
|--------|-----------|
| **Hero** | Chamada principal com badge “Profissionais Verificados” e CTA para serviços |
| **Diferenciais** | Cards: profissionais verificados, agendamento rápido, garantia e pagamento seguro |
| **Como funciona** | Fluxo em 3 passos (escolher serviço → receber profissional → aproveitar a casa) |
| **Catálogo de serviços** | Cards com preços e botão “Agendar” via WhatsApp |
| **Contato** | Formulário AJAX (FormSubmit) + dados de WhatsApp, e-mail e horário |
| **Rodapé** | Links rápidos, redes sociais e informações de contato |
| **WhatsApp flutuante** | Botão fixo para agendamento imediato |
| **Responsivo** | Menu mobile, grids adaptáveis e ocultação de elementos decorativos em telas menores |
| **Acessibilidade básica** | `lang="pt-BR"`, feedback do formulário com `aria-live`, campo honeypot anti-spam |

---

## Serviços exibidos (referência de preços)

Os valores abaixo são os apresentados no site; confirme sempre no WhatsApp antes de fechar o serviço.

| Serviço | Descrição resumida | Preço no site |
|---------|-------------------|---------------|
| Limpeza Básica | 1 banheiro, até 2 quartos, sala e cozinha | R$ 150,00 (padrão) |
| Limpeza Completa | 2+ banheiros, limpeza geral e organização | R$ 180,00 (a partir) |
| Faxina Pesada | Limpeza profunda e detalhada | A partir de R$ 250,00 |
| Lavagem / passar roupas | Serviço à parte | A combinar |
| Serviços extras | Armários, geladeira, janelas, etc. | A combinar |

---

## Stack tecnológica

- **HTML5** — estrutura semântica e seções com IDs para âncoras
- **CSS3** — variáveis CSS (`:root`), Grid, Flexbox, media queries e animações (`@keyframes`, `IntersectionObserver` via classes)
- **JavaScript (vanilla)** — scroll suave, navbar dinâmica, animação `fade-in`, menu mobile e envio do formulário com `fetch`
- **Fontes:** [Google Fonts](https://fonts.google.com/) — Poppins e Playfair Display
- **Ícones:** [Font Awesome 6.4](https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css) (CDN)
- **Formulário:** [FormSubmit](https://formsubmit.co/) — endpoint AJAX para `rose.faxina.contato@gmail.com`

Não há build, bundler nem dependências npm: o projeto é **100% estático** e pronto para hospedagem simples.

---

## Estrutura do repositório

```
Rose-Faxina-Site/
├── index.html         # Página principal (HTML + CSS + JS embutidos)
├── favicon.png        # Ícone do site (favicon e apple-touch-icon)
└── README.md          # Este arquivo
```

Todo o estilo e o script estão no próprio `index.html`, o que facilita deploy em GitHub Pages ou qualquer host de arquivos estáticos.

---

## Como executar localmente

1. **Clone o repositório:**

   ```bash
   git clone https://github.com/melker22/Rose-Faxina-Site.git
   cd Rose-Faxina-Site
   ```

2. **Abra a página no navegador:**

   - Dê duplo clique em `index.html`, ou
   - Use uma extensão “Live Server” no VS Code / Cursor, ou
   - Sirva com um servidor local (recomendado para testar o formulário sem restrições de CORS em alguns cenários):

   ```bash
   # Python 3
   python -m http.server 8080

   # Node.js (se tiver npx)
   npx serve .
   ```

   Acesse: `http://localhost:8080/` (o servidor abre `index.html` automaticamente na raiz)

3. **Teste o formulário:** na primeira utilização do FormSubmit, pode ser necessário **confirmar o e-mail** `rose.faxina.contato@gmail.com` através do link enviado pelo serviço.

---

## Deploy (GitHub Pages)

O repositório usa **`index.html`** na raiz e o workflow `.github/workflows/deploy-pages.yml`.

1. Faça push na branch `main`.
2. No GitHub: **Settings → Pages → Build and deployment → Source:** escolha **GitHub Actions**.
3. Em **Actions**, confira se o job “Deploy GitHub Pages” terminou com sucesso.
4. O site ficará em: **https://melker22.github.io/Rose-Faxina-Site/**

Se a URL retornar 404, o Pages ainda não foi ativado ou o workflow não rodou — veja [COMO-TESTAR-FORMULARIO.md](COMO-TESTAR-FORMULARIO.md).

**Formulário:** antes do primeiro envio real, ative o link que o FormSubmit manda para `rose.faxina.contato@gmail.com` (detalhes no guia acima).

**Produção (HostGator):** configure os secrets FTP e use o workflow `deploy-hostgator.yml` — guia completo em [DEPLOY-AUTOMATICO.md](DEPLOY-AUTOMATICO.md).

Alternativas: upload manual no cPanel, Netlify, Vercel ou Cloudflare Pages.

---

## Personalização

### Cores e tipografia

As cores principais estão em variáveis no bloco `:root` dentro de `index.html`:

```css
--primary-pink: #E8B4CB;
--secondary-pink: #D4A5B5;
--deep-purple: #8B7B9E;
/* ... */
```

Altere esses valores para ajustar a identidade visual sem buscar cores espalhadas pelo arquivo.

### WhatsApp

Links de agendamento usam o número internacional:

`https://wa.me/5564999601220`

Substitua `5564999601220` em todos os `href` que apontam para `wa.me` (navbar, cards de serviço, rodapé e botão flutuante).

### Formulário de contato

- **Action:** `https://formsubmit.co/ajax/rose.faxina.contato@gmail.com`
- **Campos ocultos:** `_subject`, `_template`, `_captcha`, `_replyto`
- **Anti-spam:** campo `_honey` (honeypot)

Para trocar o e-mail de destino, altere a URL em `action` do `<form id="contact-form">` e confirme o novo endereço no painel do FormSubmit.

### Redes sociais

No rodapé:

- Instagram: `https://www.instagram.com/rosefaxina.servicos/`
- Facebook: perfil configurado no HTML
- WhatsApp: mesmo link acima

---

## Seções da página (âncoras)

| ID | Seção |
|----|--------|
| `#home` | Hero |
| `#recursos` | Por que escolher a Rose |
| `#como-funciona` | Passo a passo |
| `#servicos` | Catálogo e preços |
| `#contato` | Formulário e canais |

A navegação fixa usa scroll suave via JavaScript para esses IDs.

---

## Contato oficial (negócio)

| Canal | Informação |
|-------|------------|
| **WhatsApp** | [(64) 99960-1220](https://wa.me/5564999601220) |
| **E-mail** | rose.faxina.contato@gmail.com |
| **Instagram** | [@rosefaxina.servicos](https://www.instagram.com/rosefaxina.servicos/) |
| **Localização** | Mineiros, GO |
| **Atendimento** | Segunda a sábado, 7h às 20h |

---

## Segurança e privacidade

- O formulário usa **FormSubmit** (serviço de terceiros); leia a política deles antes de coletar dados pessoais em produção.
- O campo **honeypot** reduz envios automáticos de bots.
- Não commite senhas, chaves de API ou arquivos `.env` neste repositório — o site não exige backend próprio.

---

## Contribuição

1. Faça um fork do projeto.
2. Crie uma branch: `git checkout -b feature/minha-melhoria`
3. Commit suas alterações: `git commit -m "Descrição clara da mudança"`
4. Push: `git push origin feature/minha-melhoria`
5. Abra um Pull Request no repositório [melker22/Rose-Faxina-Site](https://github.com/melker22/Rose-Faxina-Site).

Para alterações de texto, preços ou links, edite diretamente `index.html` e teste em desktop e mobile.

---

## Licença

Este projeto não define um arquivo de licença no repositório. Se você for o mantenedor, considere adicionar uma licença (por exemplo, MIT) ou indicar “todos os direitos reservados” conforme a política da Rose Faxina.

---

## Créditos

- **Marca:** Rose Faxina / Rose Limpeza  
- **Desenvolvimento:** site estático com foco em conversão e experiência mobile  
- **Ícones:** Font Awesome  
- **Fontes:** Google Fonts  

© Rose Limpeza — Todos os direitos reservados.
