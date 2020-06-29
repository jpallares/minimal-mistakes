---
title: Configura Jekyll para ser multi idioma sin plugins
excerpt: Multi-idioma básico alojado en Github Pages
lang: es
ref: multilanguage-jekyll
---

Han pasado casi 6 años desde que migré de [Blogger a Jekyll + Github Pages](https://juan.pallares.me/moving-to-jekyll/) y no puedo estar más contento con el cambio. Aún así, algo que quería hace tiempo es convertirlo en multi-idioma. Tengo entradas en mente que no he escrito porque el target claro es España y como bien sabemos el nivel de inglés no es alto. Este último fin de semana me he decidio y aquí os presento mi o̵b̵r̵a̵ chapuza.

## Requisitos

- **Sin plugins.** Github Pages no es compatible con muchos [plugins](https://pages.github.com/versions/). Por ejemplo, no he podido usar [jekyll-multiple-languages-plugin](https://github.com/kurtsson/jekyll-multiple-languages-plugin)
- **Compatible con Minimal Mistakes**. Mi [tema de Jekyll](https://mmistakes.github.io/minimal-mistakes/) con el cual estoy encantado.
- **Mostrar la entrada si solo esta en un idioma**. Tengo muchísimos post antiguos en castellano o en inglés que no traduciré, no tiene valor.
- **Link para cambio de idioma en cada entrada**. Si hay dos idiomas o más (no creo que llegue a escribir en catalán o italiano :smile:) que se muestre un link para cambiar de idioma.
- **Link global cambio de idioma**. Esta funcionalidad se ha caído. El plugin de paginación [jekyll-paginate](https://jekyllrb.com/docs/pagination/) no permite más de una página. Seguro hay formas de hacerlo, pero no he querido dedicar el tiempo, no me compensaba.

![jekyll-paginate disclaimer](../images/pagination_jekyll.png)

## Implementación

A juzgar por los resultados de Google, muchos guerreros han ido pero pocos han vuelto victoriosos. No hay una manera estándar de hacerlo y he cogido lo que mejor me venía de cada sitio.

### Configura _config.yaml

En el _config.yml seteamos el lenguage del site añadiendo la linea `lang: en`. Y luego creamos un fichero dentro de la carpeta `_data`que yo he llamado `i18n` con el siguiente contenido:
```
en:
  label: English
  icon: 🇬🇧
  read_it_in: "Read it in"
es:
  label: Español
  icon: 🇪🇸
  read_it_in: "Léelo en"
```

Esto nos permitirá acceder a contenido según el idioma como veremos más adelante.

### Adapta el [Front Matter](https://jekyllrb.com/docs/front-matter/) de los posts

Especifica en cada post su idioma `lang` y identificador único `ref`.

```
--
title: RDP to Windows machine with PIN login
tags: [RDP, Windows, PIN, MicrosoftAccount, login, hacks]
excerpt: Don't lose the precious hour I lost
lang: en
ref: rdp
---
```

Si dos posts comparten el mismo `ref` son el mismo post en diferentes idiomas. Algunos agrupan los posts por carpetas según el idioma, no lo he considerado necesario.

### Filtra por idioma

Mi página principal es una paginacioón de todas las entradas del blog. Ahora queremos que se muestren todos pero si están en más de un idioma que se muestren en inglés.

Antes mostraba todos los posts que venian del paginator:
{% raw %}
```
{% for post in paginator.posts %}
  {% include archive-single.html %}
{% endfor %}
```
{% endraw %}

Después lo que he hecho ha sido agrupar por el campo `ref`. De esta manera puede saber si hay más de un idioma para cada entrada ya que el grupo tendrá más de 1 item. Si ese es el caso, cojo solo el post que tiene el mismo idioma que la página (Inglés en mi caso), de lo contrario muestro el post independientemente del idioma:
{% raw %}
```
{% assign items_grouped = paginator.posts | group_by: 'ref' %}
{% for group in items_grouped %}
    {% if group.items.size > 1 %}
        {% assign post = group.items | where: "lang",page.lang | first %}
    {% else %}
        {% assign post = group.items[0] %}
    {% endif %}
    {% include archive-single.html %}
{% endfor %}
```
{% endraw %}

Ese código tan bonito es [Liquid](https://jekyllrb.com/docs/liquid/), puede que ya esté en el TOP 5 de mis lenguajes más odiados. Tened en cuenta que el sangrado lo hago yo por claridad, no es necesario. Para poder mostrar código Liquid en Jekill, escaparlo, hay que usar `raw`.

![Escape liquid code with raw tag](../images/show_liquid.png)

### Filtra por idioma

Desde el código anterior se llama a `archive-single.html` y ese código es el que vamos a editar ahora para añadir una bandera con el idioma en caso que haya una traducción del post.

{% raw %}
```
{% assign versions=site.posts | where:"ref", post.ref | sort: 'lang' %}
{% if versions.size > 1 %}
    {% for version in versions %}
        {% if version.lang != site.lang %}
            <a href="{{ version.url }}" >{{ site.data.i18n[version.lang].icon }} </a>
        {% endif %}
    {% endfor %}
{% endif %}
```
{% endraw %}

Vuelve a ser un concepto similar al anterior, la diferencia es que ahora accedemos al emoji de bandera que pusimos en el fichero `_data/i18n.yml`.

### Link a otros idiomas dentro del blog

Y yendo de fuera hacia a dentro nos queda editar `single.html` que es el `layout` de mis entradas. Añade donde creas más oportuno esto:

{% raw %}
```
{% if page.bookauthor == null and page.permalink == null %}
    {% assign versions=site.posts | where:"ref", page.ref | sort: 'lang' %}
    {% if versions.size > 1 %}
        {% for version in versions %}
            {% if version.lang != page.lang %}
                <a href="{{ version.url }}" class="{{ version.lang }}">{{ site.data.i18n[version.lang].read_it_in] }} {{ site.data.i18n[version.lang].icon }} </a>
            {% endif %}
        {% endfor %}
    {% endif %}
{% endif %}
```
{% endraw %}

En el primer `if` evito que otros layouts se vean afectados y luego prácticamente igual. La diferencia es que busco el lenguaje diferente al actual y muestro un texto localizado al lado de la bandera.

## Resultado

Estás navegando sobre él ahora mismo. También puedes ver el [código en Github](https://github.com/jpallares/minimal-mistakes).

## Esquivar el agujero negro

Todos los ingenieros que tenemos un blog/landing page sufrimos lo que llamo el agujero negro. Esto es dedicar todo el tiempo a mejorar el blog técnicamente, ahora uso Gatsby, ahora deploy en Vercel, ojo que ahora tengo Github Actions...pero no escribir nada de contenido. Este update a multi-idioma era el caldo de cultivo ideal para venirme arriba y empezar un cambio de tecnología que nunca habría acabado. 

![Black hole gif](https://i.gifer.com/GVXn.gif)

Por suerte, me definí claramente los mínimos y ahora tengo un multi-idioma básico en lugar de un proyecto con las últimas tecnologías a medias. **Entregar valor, ese debe ser el foco**. Me ha ayudado el auto-obligarme a una entreda semanal. Que productivity-hacks tienes?