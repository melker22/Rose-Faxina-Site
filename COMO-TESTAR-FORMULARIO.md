# Como testar o formulário (FormSubmit)

O formulário **não depende** da HostGator nem do GitHub para enviar e-mail: ele chama o serviço **FormSubmit** pela internet. Qualquer hospedagem que sirva `index.html` por HTTP/HTTPS serve para testar.

## Por que o GitHub Pages “não funciona”

A URL https://melker22.github.io/Rose-Faxina-Site/ estava retornando **404** porque o GitHub Pages **não estava publicado** no repositório (não havia deploy ativo).

Foi adicionado o workflow `.github/workflows/deploy-pages.yml`. Depois do push:

1. Abra o repositório no GitHub → **Settings** → **Pages**
2. Em **Build and deployment**, em **Source**, escolha **GitHub Actions** (não “Deploy from a branch” se o workflow já existir)
3. Vá em **Actions** e confira se o workflow “Deploy GitHub Pages” concluiu com sucesso
4. Aguarde alguns minutos e acesse de novo a URL do Pages

---

## Passo obrigatório: ativar o FormSubmit (uma vez)

Na primeira utilização (ou após mudar de domínio), o FormSubmit responde:

> *This form needs Activation. We've sent you an email containing an 'Activate Form' link.*

**O que fazer:**

1. Abra a caixa **rose.faxina.contato@gmail.com** (e a pasta **Spam/Lixo eletrônico**)
2. Procure e-mail do **FormSubmit**
3. Clique no link **Activate Form** / **Ativar formulário**
4. Só depois disso os envios passam a chegar no Gmail

Sem esse clique, o site pode “funcionar” visualmente, mas o formulário sempre falhará.

---

## Opção 1 — Testar no seu PC (mais rápido)

Não abra o `index.html` com duplo clique (`file://`). O FormSubmit exige um **servidor web**.

No PowerShell, na pasta do projeto:

```powershell
cd C:\Workspace\Rose-Faxina-Site
python -m http.server 8080
```

No navegador:

1. Acesse http://localhost:8080/
2. Role até **Fale Conosco**
3. Preencha nome, e-mail e envie
4. Deve aparecer a mensagem verde de sucesso e o e-mail em **rose.faxina.contato@gmail.com**

Para parar o servidor: `Ctrl+C` no terminal.

---

## Opção 2 — Testar na HostGator (igual produção)

1. No **cPanel** → Gerenciador de arquivos → `public_html`
2. Envie **index.html** e **favicon.png**
3. Ative **SSL** (Let’s Encrypt) no domínio
4. Acesse `https://seudominio.com.br`
5. Com o FormSubmit **já ativado** (passo acima), envie um teste pelo formulário

Não é necessário criar banco de dados, PHP ou e-mail SMTP na HostGator para este formulário.

---

## Opção 3 — Outros hosts gratuitos (só para teste)

Se ainda não subiu na HostGator, pode subir os mesmos dois arquivos em:

- [Netlify Drop](https://app.netlify.com/drop) (arrastar a pasta)
- [Cloudflare Pages](https://pages.cloudflare.com/) (conectar o GitHub)

O teste do formulário é o mesmo: ativar o e-mail no FormSubmit → abrir o site por HTTPS → enviar o formulário.

---

## Checklist de teste

| Teste | Resultado esperado |
|--------|-------------------|
| WhatsApp (botão flutuante) | Abre conversa com (64) 99960-1220 |
| Formulário após ativação | Mensagem verde no site + e-mail no Gmail |
| Formulário sem ativação | Erro ou mensagem pedindo ativação |
| `file://` / duplo clique no HTML | FormSubmit **não** funciona |

---

## Se ainda falhar depois de ativar

1. Confirme que está acessando por **http://localhost** ou **https://seudominio** (não `file://`)
2. Teste outro navegador ou aba anônima
3. No FormSubmit, verifique se o domínio novo precisa ser liberado (painel em https://formsubmit.co)
4. Use o WhatsApp como canal alternativo — já funciona sem FormSubmit
