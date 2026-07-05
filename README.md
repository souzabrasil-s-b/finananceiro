# Livro-Caixa — pronto para GitHub Pages, Firebase e PWABuilder   

Esta pasta já está pronta para virar um app instalável. Contém:

- `index.html` — o app (com manifest, ícones e service worker já ligados)
- `manifest.json` — configuração do PWA (nome, ícones, cores)
- `sw.js` — service worker (permite abrir offline depois da primeira visita)
- `icon-192.png`, `icon-512.png`, `icon-512-maskable.png` — ícones do app

⚠️ Importante: os dados do app ficam salvos no **localStorage do navegador**,
por domínio. Ou seja, uma vez publicado em uma URL (GitHub Pages ou Firebase),
os dados serão os mesmos em qualquer aparelho que acessar aquela URL e salvar
ali — mas não vão se misturar com o que você já testou localmente abrindo o
arquivo direto do celular.

---

## 1. Subir para o GitHub

1. Crie um repositório novo em https://github.com/new (ex: `livro-caixa`).
   Marque como público (necessário para GitHub Pages gratuito).
2. No seu computador (ou no app GitHub / Termux no celular), dentro desta pasta:

```bash
git init
git add .
git commit -m "Livro-Caixa: primeiro commit"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/livro-caixa.git
git push -u origin main
```

3. Ative o GitHub Pages: no repositório, vá em **Settings → Pages**, em
   "Branch" escolha `main` e a pasta `/ (root)`, e salve.
   Em alguns minutos o app estará em:
   `https://SEU-USUARIO.github.io/livro-caixa/`

Isso já é suficiente para testar como PWA e também para usar no PWABuilder.

---

## 2. Deploy no Firebase Hosting (alternativa ou além do GitHub Pages)

1. Instale o Firebase CLI (uma vez só no seu computador):
```bash
npm install -g firebase-tools
```
2. Faça login (abre o navegador):
```bash
firebase login
```
3. Dentro desta pasta, inicialize o Hosting:
```bash
firebase init hosting
```
   - Escolha "Use an existing project" (crie um projeto antes em
     https://console.firebase.google.com se ainda não tiver) ou crie um novo.
   - Pasta pública: aponte para esta mesma pasta (ou copie estes arquivos
     para a pasta `public` que o Firebase criar).
   - "Configure as a single-page app": responda **No**.
   - Não sobrescreva o `index.html` se ele perguntar.
4. Deploy:
```bash
firebase deploy
```
   Você receberá uma URL tipo `https://SEU-PROJETO.web.app`.

---

## 3. Gerar o app com PWABuilder

1. Acesse https://www.pwabuilder.com
2. Cole a URL publicada (do GitHub Pages ou do Firebase) e clique em "Start".
3. O PWABuilder vai analisar o `manifest.json` e o `sw.js` automaticamente
   (por isso a URL precisa estar publicada e acessível pela internet).
4. Na aba "Android", gere o pacote (.apk/.aab) para publicar na Play Store
   ou instalar direto no celular. Nas abas "iOS" e "Windows" você também
   consegue gerar os respectivos pacotes.
5. Se o PWABuilder apontar algo faltando (ex: mais tamanhos de ícone),
   ele mesmo sugere e gera os arquivos que faltarem.

---

## Dica de manutenção

Sempre que eu (ou você) alterar o `index.html`, é só repetir o `git push`
(GitHub) e/ou `firebase deploy` — a URL final não muda, então o PWABuilder
e o app instalado nos celulares vão pegar a versão nova automaticamente
(o service worker atualiza o cache a cada nova visita).
