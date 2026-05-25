# G. Studios — Portfolio

Portfólio cinematográfico no estilo Netflix, com carrosséis horizontais por categoria.

> **Acesso aberto:** a tela de senha está desativada por enquanto. O arquivo `_login-backup.html` mantém a versão antiga (apenas como backup, não é usado pelo site). Quando quiser reativar a senha, é só me pedir.

---

## 📁 Estrutura dos arquivos

```
portfolio/
├── index.html              → O portfólio (página principal)
├── _login-backup.html      → Tela de senha (BACKUP, desativada)
├── README.md               → Este arquivo
└── assets/
    ├── logo.png            → Sua logo
    └── profile.png         → Sua foto
```

---

## 🎬 PARTE 1 — Como subir seus vídeos (Vimeo grátis)

**Por que Vimeo e não YouTube?** YouTube comprime agressivamente o vídeo (perde qualidade). Vimeo preserva muito melhor a qualidade original e ainda permite player limpo (sem anúncios, sem "vídeos recomendados" no fim).

### Passo a passo:

1. Crie conta grátis em https://vimeo.com (plano "Free")
2. Clique em **Upload** → escolha o vídeo
3. Após o upload, abra o vídeo e clique em **Settings** (engrenagem)
4. Em **Privacy**:
   - "Who can watch?" → escolha **Hide from Vimeo.com** (não aparece no site público do Vimeo)
   - "Where can this be embedded?" → **Specific domains** e adicione `seu-usuario.github.io`
5. Em **Embed** → personalize o player (esconda o título, byline, etc.)
6. Clique em **Share** → copie o código `<iframe>` em "Embed"

### Como colocar o vídeo no site:

Abra `portfolio.html`, encontre o bloco do projeto e localize esta parte:

```html
<div class="placeholder">
  <svg ...></svg>
  <span>Cole aqui<br>embed Vimeo 16:9</span>
</div>
```

**Substitua TODO esse `<div class="placeholder">...</div>` pelo iframe do Vimeo:**

```html
<iframe
  src="https://player.vimeo.com/video/123456789?title=0&byline=0&portrait=0"
  allow="autoplay; fullscreen; picture-in-picture"
  allowfullscreen>
</iframe>
```

> **Limites do Vimeo grátis:** 500 MB por semana, 5 GB total. Para um portfólio enxuto com seus melhores trabalhos isso é mais que suficiente. Se precisar de mais, o plano Starter sai por ~US$ 7/mês.

---

## 🔐 PARTE 2 — Como editar a SENHA

Abra `index.html`, procure por:

```javascript
const SENHA_CORRETA = "filmmaker2026";
```

Troque `filmmaker2026` pela senha que quiser.

> ⚠️ **Importante sobre segurança:** essa senha é "client-side" — funciona como uma porta com cadeado de bicicleta, suficiente pra impedir acesso casual e proteger seu portfólio de clientes/recrutadores. Alguém tecnicamente avançado consegue burlar abrindo o código-fonte. Para portfólio profissional isso é o padrão e funciona muito bem. Se você quer segurança REAL (criptografia), veja a Parte 5.

---

## 🚀 PARTE 3 — Como subir no GitHub Pages

### 1) Criar o repositório

1. Crie conta em https://github.com (se não tiver)
2. Clique no `+` → **New repository**
3. Nome do repositório: `portfolio` (ou o nome que preferir)
4. Marque **Public** (Pages grátis só funciona em repos públicos)
5. **Create repository**

### 2) Subir os arquivos

**Opção A — pelo navegador (mais fácil):**

1. No repositório recém-criado, clique em **uploading an existing file**
2. Arraste TODOS os arquivos desta pasta (`index.html`, `portfolio.html`, `README.md` e a pasta `assets/` inteira)
3. Clique em **Commit changes**

**Opção B — pelo terminal:**

```bash
cd portfolio
git init
git add .
git commit -m "primeiro deploy"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/portfolio.git
git push -u origin main
```

### 3) Ativar o GitHub Pages

1. No repositório, vá em **Settings** (aba superior)
2. Menu lateral: **Pages**
3. Em "Source", escolha: **Deploy from a branch**
4. Em "Branch", escolha: **main** + pasta `/ (root)`
5. **Save**

Em ~1 minuto seu site estará em:
**`https://SEU-USUARIO.github.io/portfolio/`**

---

## ✏️ PARTE 4 — Como adicionar/editar projetos

O portfólio agora funciona estilo **Netflix**: hero compacto, banner de destaque, e **carrosséis horizontais por categoria** que aparecem automaticamente. Adicionar um projeto agora é muito mais fácil — você só edita um objeto em uma lista, e o carrossel certo aparece sozinho.

### Onde editar:

Abra `portfolio.html` e procure por:

```javascript
const PROJECTS = [
  ...
];
```

Cada projeto é um objeto. Para adicionar um novo, copie um objeto existente e cole no final da lista (antes do `];`):

```javascript
{
  id: 'p05',                                  // ID único (p05, p06, p07...)
  title: 'Nome do Projeto Aqui',
  year: '2026',
  client: 'Nome do Cliente',
  categories: ['marketing','social'],         // veja lista abaixo
  format: 'h',                                // 'h' | 'v' | 'both'
  videos: { h: '123456789' },                 // ID do Vimeo (só o número da URL)
  roles: ['Direção de fotografia','Edição'],
  desc: 'Descrição do trabalho aqui. Pode ter vários parágrafos.',
  meta: {
    'Cliente': 'Nome aqui',
    'Plataforma': 'Instagram',
    'Duração': '1:30 min'
    // pode adicionar quantos campos quiser
  }
}
```

### Formatos de vídeo:

```javascript
// Só horizontal
format: 'h',
videos: { h: '123456789' }

// Só vertical
format: 'v',
videos: { v: '987654321' }

// Mesmo projeto com versão horizontal E vertical
format: 'both',
videos: { h: '123456789', v: '987654321' }
```

### Categorias disponíveis:

Um projeto pode ter **várias categorias** (uma só, ou mistura):

| Slug | Aparece como |
|------|------------------------|
| `marketing` | Ações de Marketing |
| `eventos` | Cobertura de Eventos |
| `sameday` | Same Day Edit |
| `mobile` | Mobile |
| `institucional` | Institucional |
| `videoclipes` | Videoclipes |
| `social` | Mídias Sociais |

**Exemplos:**
```javascript
categories: ['marketing','social']           // aparece em 2 carrosséis
categories: ['videoclipes']                  // só em videoclipes
categories: ['eventos','sameday','social']   // aparece em 3
```

**Importante:** o mesmo projeto aparece em todos os carrosséis das categorias que você listar. Os carrosséis com 0 projetos somem automaticamente.

### Onde está o ID do Vimeo?

Na URL: `https://vimeo.com/1195173058` → o ID é `1195173058`.

### Trocar o vídeo do banner (Featured):

Procure no HTML por `id="featuredFrame"` e troque o ID na URL do iframe. Também ajuste o título e descrição logo abaixo.

---

## 🔒 PARTE 5 — (Opcional) Senha CRIPTOGRAFADA com StatiCrypt

Se você quer que NEM o código-fonte revele os conteúdos sem a senha, use StatiCrypt. Ele criptografa o HTML inteiro — sem a senha, ninguém consegue ler nada.

### Como usar:

1. Acesse https://www.staticrypt.com/
2. Faça upload do `portfolio.html`
3. Defina sua senha
4. Baixe o arquivo criptografado (vem como `portfolio.html`)
5. Substitua o `portfolio.html` original pelo criptografado
6. **Importante:** com StatiCrypt, você pode até DELETAR o `index.html` e usar só o `portfolio.html` (renomeie para `index.html`) — a tela de senha vem embutida pelo próprio StatiCrypt.

> Se usar StatiCrypt, todo conteúdo (incluindo links do Vimeo) fica criptografado de verdade. É o nível de segurança usado por estúdios profissionais.

---

## 🎨 Personalizações rápidas

### Trocar cores (em ambos os arquivos, dentro de `:root`):

```css
:root {
  --bg: #0F2A30;        /* azul-petróleo profundo */
  --bg-deep: #081A1E;   /* mais escuro (footer) */
  --ink: #E8E2D5;       /* off-white quente */
  --accent: #C7A87A;    /* dourado dessaturado */
  --accent-2: #4A8B92;  /* turquesa apagado */
  --accent-3: #B89968;  /* dourado profundo */
  --muted: #7A8A8C;     /* azul-acinzentado */
}
```

### Trocar a logo / foto:
Substitua os arquivos em `assets/logo.png` e `assets/profile.png` mantendo os mesmos nomes.

### Trocar contato no footer:
Em `portfolio.html`, procure `contato@gstudios.com` e os links de redes sociais — edite à vontade.

---

## ✅ Checklist final antes de mandar pra clientes

- [ ] Trocou a senha em `index.html`
- [ ] Subiu todos os vídeos no Vimeo (com domínio configurado)
- [ ] Substituiu os placeholders pelos iframes do Vimeo
- [ ] Editou títulos, descrições, anos e funções de cada projeto
- [ ] Atualizou e-mail e redes no footer
- [ ] Subiu no GitHub Pages
- [ ] Testou em desktop E celular
- [ ] (Opcional) Aplicou StatiCrypt para criptografia real

---

Qualquer dúvida na hora de implementar, é só perguntar. Boa sorte com os trabalhos! 🎬
