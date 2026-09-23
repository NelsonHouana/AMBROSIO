# Ligar o convite ao GitHub (e publicar no GitHub Pages)

O convite já está pronto para GitHub: é um site estático (`index.html` + `js/invite.js`),
não precisa de servidor, base de dados nem instalação de nada.

---

## Opção A — Pela página do GitHub (sem comandos, a mais simples)

1. Crie um repositório novo em <https://github.com/new>
   - Nome sugerido: `convite-maria-lina-ambrosio`
   - Visibilidade: **Public** (necessário para GitHub Pages gratuito)
   - **Não** marque «Add a README» (já temos um)
2. No repositório, clique em **Add file → Upload files**.
3. Arraste **todos** estes ficheiros/pastas:
   - `index.html`
   - `js/` (a pasta inteira, com `invite.js` dentro)
   - `README.md`, `.nojekyll`, `.gitignore`
   - a pasta `.github/` (opcional, ver secção «Publicação automática»)
4. Escreva uma mensagem (ex.: «Convite digital — versão inicial») e clique **Commit changes**.
5. Active o site: **Settings → Pages**
   - Em **Source**, escolha **Deploy from a branch**
   - **Branch**: `main` · **Folder**: `/ (root)` → **Save**
6. Aguarde 1–2 minutos. O endereço público aparece em **Settings → Pages**, no formato:
   ```
   https://SEU-UTILIZADOR.github.io/convite-maria-lina-ambrosio/
   ```
7. Copie esse endereço e cole-o no convite, no painel dos anfitriões
   (🔒 → código `17102026`) → **«Endereço do convite publicado»** → *Guardar endereço*.

---

## Opção B — Com Git (linha de comandos)

No terminal, dentro da pasta do projecto:

```bash
git init
git add .
git commit -m "Convite digital Maria Lina & Ambrosio"
git branch -M main
git remote add origin https://github.com/SEU-UTILIZADOR/convite-maria-lina-ambrosio.git
git push -u origin main
```

Depois, no GitHub: **Settings → Pages → Source: Deploy from a branch → main / (root) → Save**.

---

## Publicação automática (opcional)

O ficheiro `.github/workflows/deploy-pages.yml` já está incluído: sempre que fizer
um novo `push` para a branch `main`, o GitHub publica o site sozinho.

Para usar esta via, em **Settings → Pages → Source** escolha **GitHub Actions**
(em vez de «Deploy from a branch»). Se preferir a Opção A/B, pode simplesmente
apagar a pasta `.github/`.

---

## Domínio próprio (opcional)

Se quiser algo como `convite.marialinaambrosio.com`:

1. Compre/tenha o domínio.
2. Em **Settings → Pages → Custom domain**, escreva o domínio e **Save**
   (o GitHub cria automaticamente um ficheiro `CNAME` no repositório).
3. No seu fornecedor de DNS, crie os registos indicados pelo GitHub
   (normalmente 4 registos `A` para o domínio raiz, ou um `CNAME` para `www`).
4. Marque **Enforce HTTPS**.
5. Actualize o campo **«Endereço do convite publicado»** no painel do convite
   para o domínio novo.

---

## Depois de publicar — não esquecer

- **Actualizar o endereço no painel** (passo 7). Sem isto, os links gerados
  apontam para o ficheiro local e não abrem nos telemóveis dos convidados.
- **Os links gerados antes** de acertar o endereço devem ser gerados de novo
  (basta voltar a copiar/enviar).
- **A lista de convidados fica guardada no navegador** onde foi criada. Se mudar
  de telemóvel ou computador, exporte a lista (**⬇ Exportar lista (CSV)**) para
  não perder os nomes e as mesas.
- O convite publicado é **público**: qualquer pessoa com o link o pode ver.
  O código `17102026` do painel é apenas uma barreira simples do lado do
  navegador — **não é segurança real**.

---

## Verificação rápida depois do deploy

1. Abra `https://SEU-UTILIZADOR.github.io/convite-maria-lina-ambrosio/`
   → deve aparecer a foto do casal, os nomes e a data.
2. Acrescente `?convidado=Teste&mesa=Renovação` ao endereço
   → deve aparecer «Teste» no convite e «RENOVAÇÃO» na secção da mesa.
3. Entre no painel (🔒 → `17102026`), adicione um convidado de teste e use 👁
   para pré-visualizar o link.
