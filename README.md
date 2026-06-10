# Central de Solicitações — Dashboard

Painel de gestão municipal de zeladoria urbana, em HTML e CSS puro (sem frameworks nem dependências externas).

## Estrutura de arquivos

```
.
├── index.html        # marcação da página
├── css/
│   └── style.css     # todo o estilo, dividido em seções
└── README.md
```

O HTML carrega o estilo por um único link no `<head>`:

```html
<link rel="stylesheet" href="css/style.css">
```

Para rodar, basta abrir o `index.html` no navegador. Mantenha a pasta `css/` ao lado do HTML.

## Como o CSS está organizado

O `style.css` segue uma ordem do geral para o específico. Cada seção é separada por um comentário em bloco (`/* ===== NOME ===== */`), então dá pra navegar com Ctrl+F pelo nome da seção.

| # | Seção | O que controla |
|---|-------|----------------|
| 1 | **Tokens de design** (`:root`) | Variáveis de cor, raio de borda e sombra. É o ponto central de customização. |
| 2 | **Reset** | `* { margin/padding/box-sizing }` e estilo base do `body`. |
| 3 | **Sidebar** | Menu lateral fixo: marca, navegação e cartão de usuário. |
| 4 | **Área principal** | Topbar, breadcrumb e wrapper do conteúdo. |
| 5 | **KPI cards** | Os 4 cartões de indicadores do topo. |
| 6 | **Grid principal** | A divisão em duas colunas (gráficos + alertas). |
| 7 | **Gráfico de barras** | Evolução temporal feita em CSS puro (eixo, grade, colunas, tooltip). |
| 8 | **Alertas recentes** | Lista lateral com bolinha de severidade e tags. |
| 9 | **Responsivo** | `@media` para tablet e celular. |

## Sistema de tokens

Toda cor e medida repetida vive como variável CSS no `:root`. Para reestilizar, edite num lugar só:

```css
:root {
  --azul-escuro: #1a2942;   /* sidebar e headers */
  --verde: #1ba672;         /* indicadores positivos */
  --vermelho: #e63946;      /* alertas críticos */
  --raio: 12px;             /* arredondamento dos cards */
}
```

Trocar a identidade visual inteira é questão de mudar esses valores — nada precisa ser caçado pelo resto do arquivo.

## Convenções

- **Classes de cor por variante.** Componentes que mudam só de cor usam uma classe modificadora: `.kpi.azul`, `.kpi.vermelho`, `.dot.laranja`, `.tag.urg`. A estrutura é a mesma; a variante só troca a cor.
- **Larguras de barra por classe.** As barras de progresso (`.f1`–`.f4`) e as colunas do gráfico (`.b1`–`.b6`) têm a altura/largura fixada por classe, em vez de estilo inline, pra manter o HTML limpo.
- **Layout em flex e grid.** A casca (`.app`) é flex; os blocos de cartões (`.kpi-grid`, `.grid-main`, `.analise-body`) são grid. Cada um tem seu próprio `@media` de quebra.
- **Sem !important.** A especificidade é mantida baixa e previsível, então qualquer ajuste pontual sobrescreve sem brigar.

## Onde mexer para tarefas comuns

- **Mudar uma cor do tema** → seção 1, bloco `:root`.
- **Editar o menu lateral** → `index.html` (lista `.nav`) + seção 3 do CSS.
- **Ajustar os números dos KPIs** → direto no `index.html`, dentro de `.kpi-value`.
- **Alterar a altura das colunas do gráfico** → classes `.b1`–`.b6` na seção 7.
- **Ponto de quebra mobile** → seção 9 (`@media`).

## Notas

- Os ícones são caracteres unicode/emoji usados como placeholder. Para produção, troque por uma biblioteca de ícones SVG (Lucide, Font Awesome).
- Os dados são estáticos no HTML. Para torná-los dinâmicos, alimente os elementos via JavaScript/API.