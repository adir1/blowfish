---
title: "Shortcodes"
date: 2020-08-11
draft: false
description: "All the shortcodes available in Blowfish."
slug: "shortcodes"
tags: ["shortcodes", "mermaid", "icon", "lead", "docs"]
series: ["Documentation"]
series_order: 8
---

In addition to all the [default Hugo shortcodes](https://gohugo.io/content-management/shortcodes/), Blowfish adds a few extras for additional functionality.

## Alert

`alert` outputs its contents as a stylised message box within your article. It's useful for drawing attention to important information that you don't want the reader to miss.

The input is written in Markdown so you can format it however you please.

By default, the alert is presented with an exclaimation triangle icon. To change the icon, include the icon name in the shortcode. Check out the [icon shortcode](#icon) for more details on using icons.

**Example:**

```md
{{</* alert */>}}
**Warning!** This action is destructive!
{{</* /alert */>}}

{{</* alert "twitter" */>}}
Don't forget to [follow me](https://twitter.com/nunocoracao) on Twitter.
{{</* /alert */>}}
```

{{< alert >}}
**Warning!** This action is destructive!
{{< /alert >}}
&nbsp;
{{< alert "twitter" >}}
Don't forget to [follow me](https://twitter.com/nunocoracao) on Twitter.
{{< /alert >}}

## Article
`Article` will embed a single article into a markdown file. The `link` to the file should be the `.RelPermalink` of the file to be embedded. Note that the shortcode will not display anything if it's referencing it's parent. *Note: if you are running your website in a subfolder like Blowfish (i.e. /blowfish/) please include that path in the link.*

<!-- prettier-ignore-start -->
| Parameter | Description                                              |
| --------- | -------------------------------------------------------- |
| `link`    | **Required.** the `.RelPermalink` to the target article. |
<!-- prettier-ignore-end -->

**Example:**

```md
{{</* article link="/blowfish/docs/welcome/" */>}}
```

{{< article link="/blowfish/docs/welcome/" >}}



## Badge

`badge` outputs a styled badge component which is useful for displaying metadata.

**Example:**

```md
{{</* badge */>}}
New article!
{{</* /badge */>}}
```

{{< badge >}}
New article!
{{< /badge >}}

## Button

`button` outputs a styled button component which can be used to highlight a primary action. It has two optional variables `href` and `target` which can be used to specify the URL and target of the link.

**Example:**

```md
{{</* button href="#button" target="_self" */>}}
Call to action
{{</* /button */>}}
```

{{< button href="#button" target="_self" >}}
Call to action
{{< /button >}}

## Chart

`chart` uses the Chart.js library to embed charts into articles using simple structured data. It supports a number of [different chart styles](https://www.chartjs.org/docs/latest/samples/) and everything can be configured from within the shortcode. Simply provide the chart parameters between the shortcode tags and Chart.js will do the rest.

Refer to the [official Chart.js docs](https://www.chartjs.org/docs/latest/general/) for details on syntax and supported chart types.

**Example:**

```js
{{</* chart */>}}
type: 'bar',
data: {
  labels: ['Tomato', 'Blueberry', 'Banana', 'Lime', 'Orange'],
  datasets: [{
    label: '# of votes',
    data: [12, 19, 3, 5, 3],
  }]
}
{{</* /chart */>}}
```

<!-- prettier-ignore-start -->
{{< chart >}}
type: 'bar',
data: {
  labels: ['Tomato', 'Blueberry', 'Banana', 'Lime', 'Orange'],
  datasets: [{
    label: '# of votes',
    data: [12, 19, 3, 5, 3],
  }]
}
{{< /chart >}}
<!-- prettier-ignore-end -->

You can see some additional Chart.js examples on the [charts samples]({{< ref "charts" >}}) page.

## Figure

Blowfish includes a `figure` shortcode for adding images to content. The shortcode replaces the base Hugo functionality in order to provide additional performance benefits.

When a provided image is a page resource, it will be optimised using Hugo Pipes and scaled in order to provide images appropriate to different device resolutions. If a static asset or URL to an external image is provided, it will be included as-is without any image processing by Hugo.

The `figure` shortcode accepts six parameters:

<!-- prettier-ignore-start -->
| Parameter | Description                                                                                                                                                                                                                                                                                                                                                                               |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `src`     | **Required.** The local path/filename or URL of the image. When providing a path and filename, the theme will attempt to locate the image using the following lookup order: Firstly, as a [page resource](https://gohugo.io/content-management/page-resources/) bundled with the page; then an asset in the `assets/` directory; then finally, a static image in the `static/` directory. |
| `alt`     | [Alternative text description](https://moz.com/learn/seo/alt-text) for the image.                                                                                                                                                                                                                                                                                                         |
| `caption` | Markdown for the image caption, which will be displayed below the image.                                                                                                                                                                                                                                                                                                                  |
| `class`   | Additional CSS classes to apply to the image.                                                                                                                                                                                                                                                                                                                                             |
| `href`    | URL that the image should be linked to.                                                                                                                                                                                                                                                                                                                                                   |
| `default` | Special parameter to revert to default Hugo `figure` behaviour. Simply provide `default=true` and then use normal [Hugo shortcode syntax](https://gohugo.io/content-management/shortcodes/#figure).                                                                                                                                                                                       |
<!-- prettier-ignore-end -->

Blowfish also supports automatic conversion of images included using standard Markdown syntax. Simply use the following format and the theme will handle the rest:

```md
![Alt text](image.jpg "Image caption")
```

**Example:**

```md
{{</* figure
    src="abstract.jpg"
    alt="Abstract purple artwork"
    caption="Photo by [Jr Korpa](https://unsplash.com/@jrkorpa) on [Unsplash](https://unsplash.com/)"
    */>}}

<!-- OR -->

![Abstract purple artwork](abstract.jpg "Photo by [Jr Korpa](https://unsplash.com/@jrkorpa) on [Unsplash](https://unsplash.com/)")
```

{{< figure src="abstract.jpg" alt="Abstract purple artwork" caption="Photo by [Jr Korpa](https://unsplash.com/@jrkorpa) on [Unsplash](https://unsplash.com/)" >}}

## Icon

`icon` outputs an SVG icon and takes the icon name as its only parameter. The icon is scaled to match the current text size.

**Example:**

```md
{{</* icon "github" */>}}
```

**Output:** {{< icon "github" >}}

Icons are populated using Hugo pipelines which makes them very flexible. Blowfish includes a number of built-in icons for social, links and other purposes. Check the [icon samples]({{< ref "samples/icons" >}}) page for a full list of supported icons.

Custom icons can be added by providing your own icon assets in the `assets/icons/` directory of your project. The icon can then be referenced in the shortcode by using the SVG filename without the `.svg` extension.

Icons can also be used in partials by calling the [icon partial]({{< ref "partials#icon" >}}).

## List
`List` will display a list of recent articles. This shortcode requires a limit value to constraint the list. Additionally, it supports a `where` and a `value` in order to filter articles by their parameters. Note that this shortcode will not display its parent page but it will count for the limit value.

<!-- prettier-ignore-start -->
| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| `limit`   | **Required.** the number of recent articles to display. |
| `where`   | the number of recent articles to display.               |
| `value`   | the number of recent articles to display.               |

<!-- prettier-ignore-end -->

**Example #1:**
```md
{{</* list limit=2 */>}}
```

{{< list limit=2 >}}

**Example #2:**
```md
{{</* list limit=2 where="Type" value="sample" */>}}
```

{{< list limit=2 where="Type" value="sample">}}


## Swatches
`swatches` outputs a set of up to three different colors to showcase color elements like a color palette. This shortcode takes the `HEX` codes of each color and creates the visual elements for each.

**Example**
```md
{{</* swatches "#64748b" "#3b82f6" "#06b6d4" */>}}
```

**Output**
{{< swatches "#64748b" "#3b82f6" "#06b6d4" >}}


## Katex

The `katex` shortcode can be used to add mathematical expressions to article content using the KaTeX package. Refer to the online reference of [supported TeX functions](https://katex.org/docs/supported.html) for the available syntax.

To include mathematical expressions in an article, simply place the shortcode anywhere with the content. It only needs to be included once per article and KaTeX will automatically render any markup on that page. Both inline and block notation are supported.

Inline notation can be generated by wrapping the expression in `\\(` and `\\)` delimiters. Alternatively, block notation can be generated using `$$` delimiters.

**Example:**

```md
{{</* katex */>}}
\\(f(a,b,c) = (a^2+b^2+c^2)^3\\)
```

{{< katex >}}
\\(f(a,b,c) = (a^2+b^2+c^2)^3\\)

Check out the [mathematical notation samples]({{< ref "mathematical-notation" >}}) page for more examples.

## Lead

`lead` is used to bring emphasis to the start of an article. It can be used to style an introduction, or to call out an important piece of information. Simply wrap any Markdown content in the `lead` shortcode.

**Example:**

```md
{{</* lead */>}}
When life gives you lemons, make lemonade.
{{</* /lead */>}}
```

{{< lead >}}
When life gives you lemons, make lemonade.
{{< /lead >}}

## Mermaid

`mermaid` allows you to draw detailed diagrams and visualisations using text. It uses Mermaid under the hood and supports a wide variety of diagrams, charts and other output formats.

Simply write your Mermaid syntax within the `mermaid` shortcode and let the plugin do the rest.

Refer to the [official Mermaid docs](https://mermaid-js.github.io/) for details on syntax and supported diagram types.

**Example:**

```md
{{</* mermaid */>}}
graph LR;
A[Lemons]-->B[Lemonade];
B-->C[Profit]
{{</* /mermaid */>}}
```

{{< mermaid >}}
graph LR;
A[Lemons]-->B[Lemonade];
B-->C[Profit]
{{< /mermaid >}}

You can see some additional Mermaid examples on the [diagrams and flowcharts samples]({{< ref "diagrams-flowcharts" >}}) page.

## TypeIt

[TypeIt](https://www.typeitjs.com) is the most versatile JavaScript tool for creating typewriter effects on the planet. With a straightforward configuration, it allows you to type single or multiple strings that break lines, delete & replace each other, and it even handles strings that contain complex HTML. 

Blowfish implements a sub-set of TypeIt features using a `shortcode`. Write your text within the `typeit` shortcode and use the following parameters to configure the behavior you want.

<!-- prettier-ignore-start -->
| Parameter          | Description                                                                                                                                        |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| `tag`              | [String] `html` tag that will be used to render the strings.                                                                                       |
| `classList`        | [String] List of `css` classes to apply to the `html` element.                                                                                     |
| `initialString`    | [String] Initial string that will appear written and will be replaced.                                                                             |
| `speed`            | [number] Typing speed, measured in milliseconds between each step.                                                                                 |
| `lifeLike`         | [boolean] Makes the typing pace irregular, as if a real person is doing it.                                                                        |
| `startDelay`       | [number] The amount of time before the plugin begins typing after being initialized.                                                               |
| `breakLines`       | [boolean] Whether multiple strings are printed on top of each other (true), or if they're deleted and replaced by each other (false).              |
| `waitUntilVisible` | [boolean] Determines if the instance will begin when loaded or only when the target element becomes visible in the viewport. The default is `true` |
| `loop`             | [boolean] Whether your strings will continuously loop after completing                                                                             |

<!-- prettier-ignore-end -->



**Example 1:**

```md
{{</* typeit */>}}
Lorem ipsum dolor sit amet 
{{</* /typeit */>}}
```

{{< typeit >}}
Lorem ipsum dolor sit amet 
{{< /typeit >}}

**Example 2:**

```md
{{</* typeit 
  tag=h1
  lifeLike=true
*/>}}
Lorem ipsum dolor sit amet, 
consectetur adipiscing elit. 
{{</* /typeit */>}}
```

{{< typeit 
  tag=h1
  lifeLike=true
>}}
Lorem ipsum dolor sit amet, 
consectetur adipiscing elit. 
{{< /typeit >}}


**Example 3:**

```md
{{</* typeit 
  tag=h3
  speed=50
  breakLines=false
  loop=true
*/>}}
Lorem ipsum dolor sit amet, 
consectetur adipiscing elit. 
{{</* /typeit */>}}
```
{{< typeit 
  tag=h3
  speed=50
  breakLines=false
  loop=true
>}}
"Frankly, my dear, I don't give a damn." Gone with the Wind (1939)
"I'm gonna make him an offer he can't refuse." The Godfather (1972)
"Toto, I've a feeling we're not in Kansas anymore." The Wizard of Oz (1939)
{{< /typeit >}}


## GitHub Card

[TypeIt](https://www.typeitjs.com) is the most versatile JavaScript tool for creating typewriter effects on the planet. With a straightforward configuration, it allows you to type single or multiple strings that break lines, delete & replace each other, and it even handles strings that contain complex HTML. 

Blowfish implements a sub-set of TypeIt features using a `shortcode`. Write your text within the `typeit` shortcode and use the following parameters to configure the behavior you want.

<!-- prettier-ignore-start -->
| Parameter | Description              |
| --------- | ------------------------ |
| `repor`     | [String] github repo in the format of `username/repo` |
                                                                       
<!-- prettier-ignore-end -->



**Example 1:**

```md
{{</* github repo="nunocoracao/blowfish" */>}}
```

{{< github repo="nunocoracao/blowfish" >}}