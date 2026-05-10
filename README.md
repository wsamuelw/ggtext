# ggtext

Rich text in ggplot2 — colour-highlighted titles, bold labels, and styled axis text using markdown in R.

## Problem

ggplot2 titles are plain text. You can't highlight a key word in red, bold a category name, or mix fonts within a single label. `ggtext` solves this by letting you use HTML/CSS markup inside `element_markdown()`.

## What's Inside

| File | What It Shows |
|------|-------------|
| `demo 1` | Colour-highlighted title — "Virginica irises" in red within a sentence |
| `demo 2` | Progressive enhancement: plain title → coloured title → bold + coloured → styled axis labels |

## Demo 1 — Highlighted Title

A bar chart where the title reads:

> **Virginica irises** have the largest average sepal width

With "Virginica irises" in red, the rest in black. The key: `element_markdown()` in `theme()`.

```r
labs(title = "<span style='color: red;'>Virginica irises</span> have the largest average sepal width") +
theme(plot.title = element_markdown())
```

![Demo 1](https://github.com/wsamuelw/ggtext/blob/main/image/demo%201.png)

## Demo 2 — Styled Titles and Axis Labels

A grouped bar chart comparing #python vs #rstats tweet categories, with:

1. **Plain title** — default ggplot2
2. **Coloured title** — #python in orange, #rstats in blue using `<span>` tags
3. **Bold + coloured** — adding `<strong>` for emphasis
4. **Coloured axis labels** — using `element_markdown()` on `axis.text.x` with `glue::glue()` to conditionally style categories

```r
# coloured title
labs(title = "<span style='color:#ff8c00'>#python</span> and 
     <span style='color:#346299'>#rstats</span>: Comparing 1,000 random tweets") +
theme(plot.title = element_markdown())

# styled axis labels
aes(x = category_with_color, ...) +
theme(axis.text.x = element_markdown())
```

![Demo 2](https://github.com/wsamuelw/ggtext/blob/main/image/demo%202.png)

## How It Works

`ggtext` extends ggplot2 with two key functions:

**`element_markdown()`** — drop-in replacement for `element_text()` that renders HTML/CSS:

```r
theme(
  plot.title = element_markdown(),     # title supports HTML
  axis.text.x = element_markdown()    # axis labels support HTML
)
```

**Inline HTML** — use `<span>`, `<strong>`, `<i>`, and CSS directly in labels:

```r
labs(title = "<span style='color:red;font-size:20px'>Important</span> finding")
```

## When to Use It

- **Report titles** — draw attention to the key finding in the title itself
- **Axis labels** — colour-code categories without a legend
- **Annotations** — mix bold, italic, and colour in a single text element
- **Dashboards** — make charts self-explanatory without additional context

## Setup

```r
install.packages(c("ggtext", "ggplot2", "dplyr"))
```

## Tech Stack

- **ggtext** — HTML/CSS rendering in ggplot2 text elements
- **ggplot2** — plotting framework
- **glue** — string interpolation for dynamic HTML in axis labels
- **hrbrthemes** — `theme_ipsum()` for clean defaults (Demo 1)

## References

- [ggtext on CRAN](https://cran.r-project.org/package=ggtext)
- [Colour titles with ggtext](https://rfortherestofus.com/2020/05/color-titles-ggtext/)
- [Add colour to ggplot2 text](https://www.infoworld.com/article/3527449/add-color-to-your-ggplot2-text-in-r.html)

## License

MIT
