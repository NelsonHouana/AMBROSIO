# Convite Digital — Maria Lina & Ambrósio (17.10.2026)

Convite digital de casamento (Bodas de Prata) com **personalização por convidado** e **confirmação de presença por WhatsApp**.

O design, as imagens, a música e todos os conteúdos originais do convite foram **mantidos exactamente como estavam** — apenas foram corrigidas as funcionalidades de personalização (nome do convidado + mesa) e de geração de links.

---

## 1. O que foi corrigido

O ficheiro original era um HTML autónomo (7,6 MB) com imagens e áudio embutidos em base64 e dois scripts inline que já não funcionavam:

| Problema no ficheiro original | Correção aplicada |
|---|---|
| «Gerar link / baixar HTML» descarregava um ficheiro — impossível de enviar por WhatsApp como link | Agora gera um **link real** (`?convidado=…&mesa=…`) que pode ser copiado e enviado |
| Nome e mesa ficavam guardados em `localStorage`, mas o link gerado **não os incluía** | O link transporta o nome e a mesa; quem abre o link vê o convite já personalizado |
| Não existia forma de gerir vários convidados | **Painel dos anfitriões** com lista de convidados, mesas, telemóveis e estado de envio |
| Botões de confirmação usavam um número de WhatsApp que não era o da anfitriã (`25844877321`) | Confirmações vão para o WhatsApp da anfitriã: **+258 84 753 8091** |
| Mensagens de confirmação não identificavam o convidado nem a mesa | A mensagem inclui nome do convidado e mesa |
| Dois scripts inline obsoletos, um botão duplicado, `id` duplicado no formulário de telemóvel | Scripts consolidados num ficheiro externo `js/invite.js`; IDs únicos |
| Não era possível testar/validar os links | Botão **Pré-visualizar** em cada convidado |

---

## 2. Funcionalidades concluídas

### Convite (vista do convidado)
- Hero com foto do casal, nomes e data — inalterado.
- Secções: Dedicação aos Pais, Bênção de Deus, Momento do casal, Programa do dia, Local, **A Sua Mesa**, Contagem decrescente, Dress Code, Galeria, Confirmação de presença, Rodapé.
- Nome do convidado apresentado na secção «Com a bênção de Deus» e a mesa na secção «A SUA MESA».
- Botões de confirmação (sim/não) que abrem o WhatsApp com mensagem pré-escrita, incluindo nome e mesa.
- Música de fundo, contagem decrescente para 17.10.2026 11:00 (+02:00) e animações de entrada — inalterados.

### Painel dos anfitriões (área privada)
- Abre com o botão 🔒 (canto inferior esquerdo) e código **17102026**.
- **Lista de convidados**: adicionar, editar, remover, marcar «link enviado».
- Por convidado: **copiar link**, **enviar por WhatsApp**, **pré-visualizar**, **editar**, **remover**.
- **Copiar todos os links** e **exportar lista (CSV)**.
- **Endereço do convite publicado**: campo para colar o URL público; sem ele, os links não funcionam fora do computador.
- Modal de link com o link personalizado, mensagem pronta a enviar e botões de copiar/pré-visualizar/WhatsApp.

---

## 3. Entradas funcionais (URI e parâmetros)

| Caminho | Parâmetros | Descrição |
|---|---|---|
| `index.html` | — | Convite (vista padrão) |
| `index.html` | `?convidado=<Nome>&mesa=<Mesa>` | Convite personalizado para um convidado |
| `index.html` | — | Botão 🔒 → código → painel dos anfitriões |

Exemplo de link pessoal:
```
https://<endereço-publicado>/?convidado=Marta%20e%20esposo&mesa=Renova%C3%A7%C3%A3o
```

---

## 4. Modelo de dados (armazenamento local, sem servidor)

Tudo é guardado no navegador do anfitrião (`localStorage`):

| Chave | Conteúdo |
|---|---|
| `mla_current_v1` | Convite actualmente em edição `{guest, table}` |
| `mla_guests_v1` | Lista de convidados `[{id, name, table, phone, sent}]` |
| `mla_base_url_v1` | Endereço do convite publicado |

Sem base de dados, sem servidor e sem autenticação — **não há envio automático de confirmações**: o convidado envia a confirmação pelo WhatsApp da anfitriã.

---

## 5. Configuração (em `js/invite.js`)

```js
var CONFIG = {
  defaultGuest: 'Convidado Especial',
  defaultTable: 'Renovação',
  rsvpPhone: '258847538091',   // WhatsApp que recebe as confirmações
  hostPin: '17102026',         // código do painel privado
  couple: 'Maria Lina & Ambrósio',
  dateLong: '17 de Outubro de 2026',
  weddingDate: '2026-10-17T11:00:00+02:00'
};
```

---

## 6. Estrutura de ficheiros

```
index.html      Convite (imagens e áudio embutidos em base64, como no original)
js/invite.js    Personalização, painel dos anfitriões, geração de links, RSVP
README.md       Este documento
```

---

## 7. Publicação e uso (importante)

O projecto está pronto para **GitHub + GitHub Pages** — instruções passo a passo em
[`COMO_PUBLICAR_GITHUB.md`](COMO_PUBLICAR_GITHUB.md). Ficheiros já incluídos para isso:
`.nojekyll`, `.gitignore` e `.github/workflows/deploy-pages.yml` (publicação automática).

1. **Publique** o site na aba **Publish** (ou no GitHub Pages) e copie o endereço público.
2. Abra o convite publicado, entre no painel (🔒 → `17102026`) e **cole o endereço público** no campo «Endereço do convite publicado» → *Guardar endereço*.
3. Adicione os convidados com o nome e a mesa.
4. Use 🔗 para copiar o link ou 💬 para enviar pelo WhatsApp; use 👁 para confirmar que o convite abre bem.
5. Envie o link a cada convidado — as confirmações chegam ao WhatsApp **+258 84 753 8091**.

> **Aviso:** a lista de convidados fica guardada **apenas no navegador/dispositivo** onde foi criada. Se usar outro telemóvel ou computador, a lista não aparece lá. O código do painel é apenas uma barreira simples do lado do cliente — não é segurança real (qualquer pessoa que veja o código da página pode descobri-lo), pelo que não deve guardar informação sensível.

---

## 8. Ainda não implementado (próximos passos possíveis)

- Confirmações registadas automaticamente (contagem de presenças) — exigiria um serviço externo com base de dados.
- Sincronização da lista de convidados entre dispositivos.
- Painel de estatísticas (confirmados / pendentes) alimentado pelo RSVP.
- Envio automático de mensagens em massa (o envio é manual, um a um, pelo WhatsApp).
- Galeria com mais fotos ou álbum partilhado.
