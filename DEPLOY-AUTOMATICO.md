# Deploy automático: GitHub → HostGator (FTP)

Cada **push na branch `main`** que altere `index.html` ou `favicon.png` envia os arquivos para **public_html** na HostGator usando FTP. Você não precisa mais subir manualmente pelo cPanel.

Workflow: `.github/workflows/deploy-hostgator.yml` (actions com runtime Node.js 24: `checkout@v6`, `FTP-Deploy-Action@v4.4.0`)

---

## 1. Configurar secrets no GitHub (obrigatório, uma vez)

A senha do FTP **nunca** vai no código — só nos secrets do repositório.

1. Abra: https://github.com/melker22/Rose-Faxina-Site/settings/secrets/actions  
2. **New repository secret** — crie estes três:

| Nome do secret | Valor |
|----------------|--------|
| `FTP_SERVER` | `ftp.rosefaxina.com` |
| `FTP_USERNAME` | `deploy@rosefaxina.com` |
| `FTP_PASSWORD` | Senha da conta FTP `deploy` (a que você definiu no cPanel) |

3. Salve cada um.

Sem os três secrets, o workflow falha na etapa de deploy.

---

## 2. Como atualizar o site no ar

No seu PC, depois de editar o site:

```bash
git add index.html favicon.png
git commit -m "Atualiza textos/preços do site"
git push origin main
```

1. Vá em **Actions** no GitHub e abra o workflow **Deploy to HostGator (FTP)**.  
2. Aguarde o check verde (geralmente 1–3 minutos).  
3. Abra https://rosefaxina.com.br (Ctrl+F5 para limpar cache se não notar mudança).

Também é possível rodar manualmente: **Actions** → **Deploy to HostGator (FTP)** → **Run workflow**.

---

## 3. O que é enviado (e o que não é)

**Enviado para o servidor:**

- `index.html`
- `favicon.png`

**Não enviado** (fica só no GitHub):

- `.github/`, README, guias `.md`, `.git`, etc.

---

## 4. Repositório público ou privado?

| Pergunta | Resposta |
|----------|----------|
| Precisa ser **privado** para o deploy funcionar? | **Não.** Actions funciona em repositório público ou privado. |
| Privado evita **phishing** / cópia do site? | **Parcialmente.** Quem quer copiar sua landing page pode usar **Ver código-fonte** em https://rosefaxina.com.br — o HTML público no ar é o mesmo que estaria no GitHub. Repositório privado esconde o histórico no GitHub, mas **não** esconde o site publicado. |
| O que **não** pode vazar? | A **senha FTP**. Por isso ela só existe em **GitHub Secrets**, nunca no código. |
| Recomendação prática | **Privado** se quiser menos exposição do repositório; **público** é aceitável para um site estático sem segredos no código. O essencial é: senha FTP só em secret. |

---

## 5. Git no cPanel vs GitHub Actions

| Método | Automático no push? | Observação |
|--------|---------------------|------------|
| **GitHub Actions + FTP** (este projeto) | **Sim** | Push no GitHub → deploy. Ideal para seu fluxo local → GitHub. |
| **Git Version Control no cPanel** | **Não** sozinho | Clona o repo no servidor; atualizar exige **Pull** manual ou configurar webhook/cron — mais trabalhoso. |
| **Upload manual no cPanel** | Não | O que você fazia antes. |

Para “push local → site atualizado”, **GitHub Actions + FTP** é o caminho mais direto.

---

## 6. Problemas comuns

### Workflow falhou em “Deploy site files via FTP”

- Confira os três secrets (nome exato: `FTP_SERVER`, `FTP_USERNAME`, `FTP_PASSWORD`).
- Teste login no **FileZilla** com os mesmos dados.
- No cPanel, confirme que a conta `deploy@rosefaxina.com` está ligada ao domínio e à pasta **public_html**.

### Site não mudou no navegador

- Aguarde o job ficar verde em Actions.
- Teste em aba anônima ou Ctrl+F5 (cache).

### FTPS obrigatório no plano

Se a HostGator exigir conexão segura, no workflow altere:

```yaml
protocol: ftps
```

(e, se necessário, `port: 21` ou `990` conforme o cPanel indicar).

### Quero deploy em qualquer push (incluindo só README)

No arquivo `deploy-hostgator.yml`, remova o bloco `paths:` sob `on.push`.

---

## 7. GitHub Pages (opcional)

O workflow `deploy-pages.yml` publica em `melker22.github.io/...` — é **independente** da HostGator. Você pode desativar ou ignorar o Pages se usar só **rosefaxina.com.br**.

---

## Checklist

- [ ] Secrets `FTP_SERVER`, `FTP_USERNAME`, `FTP_PASSWORD` criados no GitHub  
- [ ] Push na `main` com alteração em `index.html` ou `favicon.png`  
- [ ] Job **Deploy to HostGator (FTP)** verde em Actions  
- [ ] Site conferido em https://rosefaxina.com.br  
