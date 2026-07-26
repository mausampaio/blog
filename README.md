# Blog

Blog pessoal estático, feito com [Hugo](https://gohugo.io/) e o tema
[PaperMod](https://github.com/adityatelange/hugo-PaperMod), publicado no GitHub Pages.

- **Produção:** https://mausampaio.github.io/blog/
- **Idiomas:** Português (padrão, na raiz) e Inglês (em `/en/`)

## Requisitos

- [Hugo Extended](https://gohugo.io/installation/) v0.164.0 ou superior
- Git

No Windows: `winget install Hugo.Hugo.Extended`

## Rodando localmente

```bash
git clone --recurse-submodules git@github.com:mausampaio/blog.git
cd blog
hugo server -D
```

O site fica em http://localhost:1313/. A flag `-D` inclui os rascunhos (`draft: true`).

> Se você já clonou sem `--recurse-submodules`, rode `git submodule update --init --recursive`
> para baixar o tema.

## Estrutura

```
config/_default/     Configuração (dividida por assunto)
  hugo.toml            Config geral do site
  languages.toml       Idiomas, títulos e texto da home
  params.toml          Parâmetros do tema PaperMod
  menus.pt-br.toml     Menu do topo em português
  menus.en.toml        Menu do topo em inglês
content/pt-br/       Conteúdo em português
content/en/          Conteúdo em inglês
archetypes/          Template de front matter para posts novos
assets/css/extended/ CSS customizado (sobrescreve o tema)
static/              Arquivos servidos como estão (favicon, imagens)
themes/PaperMod/     Tema (submódulo git — não editar)
.github/workflows/   Deploy automático
```

## Escrevendo um post

```bash
hugo new content posts/meu-post.md              # português
hugo new content --contentDir content/en posts/my-post.md   # inglês
```

O arquivo nasce com `draft: true`. Para publicar, mude para `draft: false`.

### Ligando as traduções

Para o seletor de idioma apontar um post à sua tradução, use o **mesmo `translationKey`**
no front matter dos dois arquivos:

```yaml
# content/pt-br/posts/ola-mundo.md
translationKey: "hello-world"

# content/en/posts/hello-world.md
translationKey: "hello-world"
```

Posts sem par no outro idioma funcionam normalmente — só não mostram o link de tradução.

### Front matter mais usado

| Campo | Para que serve |
|---|---|
| `title` | Título do post |
| `date` | Data de publicação (ordena a listagem) |
| `draft` | `true` esconde o post do build de produção |
| `summary` | Resumo mostrado na listagem e no compartilhamento |
| `tags` / `categories` | Taxonomias, geram páginas próprias |
| `cover.image` | Imagem de capa (caminho em `static/` ou ao lado do post) |
| `ShowToc` | Mostra o índice lateral |
| `weight` | Fixa o post no topo da listagem |

## Personalizando

- **Título, descrição e texto da home:** `config/_default/languages.toml`
- **Cores, ícones sociais, opções do tema:** `config/_default/params.toml`
- **Menu do topo:** `config/_default/menus.<idioma>.toml`
- **CSS próprio:** crie arquivos em `assets/css/extended/` — o PaperMod carrega
  automaticamente, depois do CSS do tema
- **Favicon:** coloque os arquivos em `static/` (os caminhos estão em `params.toml`)

## Atualizando o tema

```bash
git submodule update --remote --merge themes/PaperMod
git commit -am "Atualiza tema PaperMod"
```

## Deploy

Todo push na branch `main` dispara o workflow em
[`.github/workflows/hugo.yml`](.github/workflows/hugo.yml), que builda o site e publica
no GitHub Pages.

**Configuração necessária uma única vez:** no repositório, vá em
*Settings → Pages → Build and deployment* e mude **Source** para **GitHub Actions**.
