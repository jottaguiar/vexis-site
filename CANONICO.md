# CANONICO — Vexis Site (institucional / marketing)

> **MD CANONICO — fonte da verdade de Vexis Site (institucional - investigar). Mexeu? Atualize AQUI.**

Ultima auditoria: 2026-06-20 · HEAD `431341d` (commit de 2026-06-08 23:02 -03) · branch `main` · remote `github.com/jottaguiar/vexis-site`.

---

## 1) Identidade e proposito

Landing page institucional / de marketing da **Vexis Tech** — o site comercial publico que apresenta o
ecossistema de credenciamento para eventos e capta leads (formulario de proposta + WhatsApp).

- Dominio alvo: **`vexistech.com.br`** (declarado em `<meta property="og:url">`).
- Publico: organizadores de eventos / produtoras (B2B e B2B2C). Tom: vendas.
- Conteudo: hero ("CREDENCIAMENTO QUE NAO PARA"), dores, comparativo de velocidade (CPF 20s vs QR 8s),
  bloco offline-first, plataforma (Credenciamento, Controle de Entrada, Chapelaria, Plenaria, Cred Local,
  Dashboard, Relatorios), add-ons (Landing Page = "Pacote"; Captacao de Leads / Sinalizacao / Face ID /
  RFID = "Em breve"), processo em 4 passos, "para quem", contato.
- **Captacao de lead**: formulario que faz POST para `api.web3forms.com` (servico SaaS de form-to-email,
  client-side, chave publica embutida — comportamento normal do Web3Forms, NAO e segredo de servidor) +
  CTA de WhatsApp (`wa.me/5541998885770` — numero comercial PUBLICO, ja exposto no site ao vivo) +
  e-mail `contato@vexistech.com.br`.
- Redes: Instagram `@vexis.tech.eventos`, LinkedIn da Vexis Tech. Rodape: "© 2026 Vexis Tech — Curitiba, PR".

> Observacao de honestidade: e uma **pagina de marketing**. As afirmacoes do site (ex.: "servidor de
> backup assume em segundos", "Cred Local = servidor reserva de prontidao") sao **copy comercial** e
> NAO refletem o estado tecnico atual do sistema — o failover de 2 nos foi **encerrado em 2026-06-09**
> (servidor unico `.10`). Ver secao 5. Quem editar o site deve evitar prometer failover ativo.

## 2) Stack

- **HTML estatico puro, arquivo unico.** Um so arquivo versionado: `index.html` (~55 KB, ~877 linhas).
  - Nada de build, bundler, framework ou `node_modules`. **Sem `package.json`, sem `README`, sem CI.**
  - CSS inline (`<style>` no `<head>`), JS vanilla inline (`<script>` no fim do `<body>`).
- Fontes: Google Fonts **Barlow** + **Barlow Condensed** (CDN) — alinhado ao brandbook.
- Cores do brandbook respeitadas: `--g:#BADCA6` `--dark:#0D0D0D` `--gray:#808080` (vars CSS no `:root`).
- Efeitos: splash interativo, parallax de hexagonos (mouse/giroscopio), scroll-snap por secao,
  IntersectionObserver para reveal e snap-dots. Tudo client-side, sem dependencia externa de JS.
- Integracao externa: **Web3Forms** (`api.web3forms.com/submit`) para o formulario de contato.

## 3) ESTADO REAL

**Status: VIVO (site estatico simples, de pagina unica).** Confirmado no codigo, nao inventado.

- E um produto entregue e funcional como landing: pagina completa, responsiva, com copy final,
  formulario funcionando (Web3Forms) e CTAs reais (WhatsApp/e-mail/Instagram/LinkedIn).
- Historia de commits coerente e recente (8 commits; ultimo 2026-06-08) — landing reescrita
  "offline-first" em `9e6d996`, ajustes de form/contato/tags ate `431341d`. Nao e abandonado.
- NAO e WIP de codigo (nao ha build pendente), MAS alguns **add-ons marcados "Em breve"** na propria
  pagina (Face ID, RFID, Captacao de Leads, Sinalizacao Digital) — sao promessas de roadmap, nao features
  do site. O site em si esta pronto.
- Nao e wrapper, stub, nem utilitario. E o site institucional real.

## 4) Versao / empacotamento

- **Nao ha versionamento de release, nem exe, nem APK, nem pipeline.** O "deploy" de um site estatico
  de 1 arquivo e publicar o `index.html`.
- **Onde esta publicado: NAO CONFIRMADO neste repo.** Nao ha `CNAME`, workflow do GitHub Actions, nem
  config de Vercel/Netlify/Pages versionado. O unico indicio e `og:url = https://vexistech.com.br`.
  Hipoteses (a verificar com o dono, fora do repo): GitHub Pages do `jottaguiar/vexis-site`, ou hospedagem
  estatica do dominio `vexistech.com.br`. **Pendencia: confirmar o host real de producao.**

## 5) Relacao com o resto do sistema Vexis

- **AUTONOMO.** Nao tem nenhuma dependencia tecnica do `.10`, do `.20`, do app Next, do admin, dos
  terminais nem do Postgres. Nao importa nada do ecossistema; nao chama API interna da Vexis. A unica
  chamada de rede e ao SaaS Web3Forms (terceiro) e fontes do Google.
- Repo separado (`vexis-site`, remote proprio no GitHub `jottaguiar`), fora do runtime do servidor.
- Relacao e **so de marca/conteudo**: descreve comercialmente os modulos que existem no ecossistema
  (credenciamento, chapelaria, plenaria, dashboard, relatorios) e o discurso offline-first.
- **Divergencias copy x realidade tecnica (2026-06-20):**
  - Site fala em "servidor de backup / Cred Local assume em segundos / servidor reserva de prontidao".
    Na realidade o **failover de 2 nos foi encerrado (2026-06-09)** → hoje e **servidor UNICO `.10`**;
    resiliencia = **offline-first nos terminais**, nao failover de servidor.
  - Admin nao e citado no site (ok); para registro: admin migrou pro `.10` (VexisAdmin :3200, Railway desligado).
- **Vendavel a parte?** E so material de venda do proprio ecossistema Vexis — nao e um produto vendido
  separadamente. Serve de funil para a proposta/orcamento.

## 6) Pendencias

- [ ] **Confirmar onde esta publicado** (GitHub Pages? host do dominio?) e documentar aqui. Adicionar
      `CNAME`/config de deploy ao repo se o host for Pages, para o deploy ficar reproduzivel.
- [ ] **Alinhar copy ao single-server**: revisar os trechos de "servidor de backup / assume em segundos /
      servidor reserva" para nao prometer failover ativo (encerrado 2026-06-09). Manter o discurso
      offline-first (esse e verdadeiro).
- [ ] Decidir o destino dos add-ons "Em breve" (Face ID, RFID, Leads, Sinalizacao) conforme o roadmap real
      (Face ID hoje e "frente nova / construir", parkado pos go-live).
- [ ] Sem `README`/`package.json`: opcional, mas um README de 5 linhas (como editar/publicar) evitaria a
      proxima "investigar".
- [ ] WhatsApp/e-mail/redes hardcoded no HTML — se mudarem, editar direto no `index.html`.

---

### Notas para quem editar
- Brandbook travado: `#0D0D0D` / `#BADCA6` / `#808080`, fonte Barlow. Zero desvio.
- Arquivo unico: toda edicao e em `C:/vexis/vexis-site/index.html`. Sem build — basta commitar/publicar.
- A `access_key` do Web3Forms no HTML e **publica por design** (chave de submissao client-side, nao da
  acesso a nada sensivel); ainda assim, qualquer chave/token de servidor NUNCA deve entrar neste arquivo
  estatico (ele e servido em claro ao publico).
