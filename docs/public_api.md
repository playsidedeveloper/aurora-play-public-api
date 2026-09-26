# Aurora Play Public API

API publica para desenvolvedores criarem lojas, vitrines e integracoes usando o catalogo da Aurora Play.

Base URL:

```txt
https://aurora-play-api.up.railway.app
```

Todas as respostas de listagem usam `list`. A rota de detalhes usa `data`.

## Item De Lista

Listagens retornam um objeto leve para reduzir trafego e custo.

```json
{
  "appId": "00000000-0000-0000-0000-000000000000",
  "title": "Nome do app",
  "developer": "Nome do desenvolvedor",
  "icon": "https://example.com/icon.png",
  "rating": "4.8",
  "size": "25 MB",
  "category": "Social",
  "type": "aplicativo"
}
```

## App Completo

Use a rota de detalhes para buscar descricao, screenshots, versao, package e listas auxiliares.

```json
{
  "appId": "00000000-0000-0000-0000-000000000000",
  "title": "Nome do app",
  "developer": "Nome do desenvolvedor",
  "icon": "https://example.com/icon.png",
  "rating": "4.8",
  "size": "25 MB",
  "category": "Social",
  "type": "aplicativo",
  "description": "Descricao do app",
  "versionName": "1.0.0",
  "versionCode": "10",
  "packageName": "com.exemplo.app",
  "screenshots": [
    { "screenshot": "https://example.com/screenshot-1.png" },
    { "screenshot": "https://example.com/screenshot-2.png" }
  ],
  "banner": "https://example.com/banner.png",
  "related": [],
  "more": [],
  "historic": []
}
```

## Home

Retorna secoes prontas para montar a pagina inicial da loja.

```bash
curl "https://aurora-play-api.up.railway.app/public/explore"
```

Resposta:

```json
{
  "success": true,
  "message": "Carregado com sucesso",
  "status": 200,
  "sections": [
    {
      "id": "home_new_releases",
      "title": "Bem-vindo(a) ao Aurora Play",
      "description": "Publicados e atualizados recentemente",
      "type": "horizontal",
      "list": [
        {
          "appId": "00000000-0000-0000-0000-000000000000",
          "title": "Nome do app",
          "developer": "Aurora Play",
          "icon": "https://example.com/icon.png",
          "rating": "4.8",
          "size": "25 MB",
          "category": "Social",
          "type": "aplicativo"
        }
      ]
    }
  ]
}
```

## Filtrar Apps

Lista apps com paginacao.

```bash
curl "https://aurora-play-api.up.railway.app/public/filter?page=1&limit=20"
```

Filtrar por tipo:

```bash
curl "https://aurora-play-api.up.railway.app/public/filter?page=1&limit=20&type=aplicativo"
curl "https://aurora-play-api.up.railway.app/public/filter?page=1&limit=20&type=jogo"
```

Filtrar por categoria:

```bash
curl "https://aurora-play-api.up.railway.app/public/filter?page=1&limit=20&type=aplicativo&categoryId=social"
curl "https://aurora-play-api.up.railway.app/public/filter?page=1&limit=20&type=jogo&categoryId=corrida"
```

Listar uma secao da home:

```bash
curl "https://aurora-play-api.up.railway.app/public/filter?page=1&limit=20&sectionKey=home_featured"
```

Parametros:

| Parametro | Tipo | Padrao | Descricao |
| --- | --- | --- | --- |
| `page` | number | `1` | Pagina atual |
| `limit` | number | `20` | Itens por pagina. Maximo: `50` |
| `type` | string | opcional | `aplicativo` ou `jogo` |
| `categoryId` | string | opcional | Categoria normalizada, como `social`, `corrida`, `educacao` |
| `sectionKey` | string | opcional | Identificador de uma secao publica da home |

Resposta:

```json
{
  "success": true,
  "message": "Apps carregados com sucesso",
  "status": 200,
  "page": 1,
  "limit": 20,
  "totalResults": 120,
  "totalPages": 6,
  "hasMore": true,
  "list": []
}
```

## Buscar Apps

Busca apps por texto.

```bash
curl "https://aurora-play-api.up.railway.app/public/search?q=whatsapp&page=1&limit=10"
```

Parametros:

| Parametro | Tipo | Padrao | Descricao |
| --- | --- | --- | --- |
| `q` | string | obrigatorio | Texto pesquisado |
| `page` | number | `1` | Pagina atual |
| `limit` | number | `10` | Itens por pagina. Maximo: `50` |

Resposta:

```json
{
  "success": true,
  "message": "Busca realizada com sucesso",
  "status": 200,
  "page": 1,
  "limit": 10,
  "totalResults": 5,
  "totalPages": 1,
  "hasMore": false,
  "list": []
}
```

## Tendencias

Retorna apps populares por downloads recentes.

```bash
curl "https://aurora-play-api.up.railway.app/public/trends/aplicativo"
curl "https://aurora-play-api.up.railway.app/public/trends/jogo"
curl "https://aurora-play-api.up.railway.app/public/trends/inicio"
```

Resposta:

```json
{
  "success": true,
  "message": "Carregado com sucesso",
  "status": 200,
  "list": []
}
```

## Detalhes Do App

Retorna os dados completos do app.

```bash
curl "https://aurora-play-api.up.railway.app/public/details/00000000-0000-0000-0000-000000000000"
```

Resposta:

```json
{
  "success": true,
  "message": "Carregado com sucesso",
  "status": 200,
  "data": {
    "appId": "00000000-0000-0000-0000-000000000000",
    "title": "Nome do app",
    "developer": "Aurora Play",
    "icon": "https://example.com/icon.png",
    "rating": "4.8",
    "size": "25 MB",
    "category": "Social",
    "type": "aplicativo",
    "description": "Descricao do app",
    "versionName": "1.0.0",
    "versionCode": "10",
    "packageName": "com.exemplo.app",
    "screenshots": [
      { "screenshot": "https://example.com/screenshot-1.png" },
      { "screenshot": "https://example.com/screenshot-2.png" }
    ],
    "banner": "https://example.com/banner.png",
    "related": [],
    "more": [],
    "historic": []
  }
}
```

## Apps Relacionados

Retorna apps semelhantes ao app informado.

```bash
curl "https://aurora-play-api.up.railway.app/public/related/00000000-0000-0000-0000-000000000000"
```

Resposta:

```json
{
  "success": true,
  "message": "Carregado com sucesso",
  "status": 200,
  "list": []
}
```

## Download Direto

Retorna a URL de download do app.

```bash
curl "https://aurora-play-api.up.railway.app/public/direct/download/00000000-0000-0000-0000-000000000000"
```

Resposta:

```json
{
  "success": true,
  "url": "https://example.com/app.apk",
  "message": "Download iniciado",
  "status": 200
}
```

Observacao: esta rota pode aplicar limite por IP e por app para evitar abuso.
