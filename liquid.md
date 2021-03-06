---
layout: page
title: Liquid
permalink: /liquid
---

[liquid](https://shopify.github.io/liquid/)


Use the hyphen {% raw %}`{{-`, `-}}`, `{%-`, and `-%}`{% endraw %} over the default to avoid unnecessary whitespace.


### SNIPPETS

Commonly used snippets for projects and/or development.

#### settings popup link

``` liquid
{%- raw -%}
{% if logged_in %}
  <a href="/pages/settings/{{ p.id }}" onclick="window.open('/pages/settings/{{ p.id }}', '_blank', 'width=600,height=650,scrollbars=yes');return false;">
    Settings
  </a>
{% endif %}
{% endraw %}
```

#### description edit form

``` liquid
{%- raw -%}
// page.liquid
// in a for loop
{% for p in page.children %}
  {% if logged_in %}
    {% assign edit_description_form_page = p %}
    {% include 'edit_description_form' %}
  {% endif %}
{% endfor %}

// as a single
{% if logged_in %}
  {% assign edit_description_form_page = page %}
  {% include 'edit_description_form' %}
{% endif %}
{% endraw %}
```

``` liquid
{%- raw -%}
// _edit_description_form.liquid
<p><a href="#" onclick="return false;" data-toggle="modal" data-target="#edit_page_{{ edit_description_form_page.id }}_modal">Edit Description</a></p>

<!-- Modal -->
<div class="modal fade" id="edit_page_{{ edit_description_form_page.id }}_modal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-body">

        <form id="edit_page_{{ edit_description_form_page.id }}">
          <div style="margin:0;padding:0;display:inline">
            <input name="utf8" type="hidden" value="✓">
            <input name="_method" type="hidden" value="patch">
          </div>

          <div class="form-group">
            <label for="page_description">Edit {{ edit_description_form_page.name }} Description</label>
            <textarea class="form-control" id="page_description" name="page[description]" rows="4">{{ edit_description_form_page.description }}</textarea>
          </div>

          <div class="form-group">
            <img alt="loading" id="spinner" src="/images/spinner_3bars_onblack.gif" style="display:none">
            <input class="btn btn-default" id="edit_page_{{ edit_description_form_page.id }}_btn" name="commit" type="submit" value="Save">
          </div>
        </form>

        <script>
          $(function() {
            var pageUrl = "/pages/settings/{{ edit_description_form_page.id }}",
              formId = "edit_page_{{ edit_description_form_page.id }}";

            var $form = $("#" + formId);

            $form.on('submit', function(e) {
              e.preventDefault();
              $('#' + formId + ' #spinner').show();
              $('#edit_page_{{ p.id }}_btn').hide();

              $.ajax({
                url: pageUrl,
                method: 'post',
                data: $form.serialize(),
                success: function(data) {
                   location.reload();
                }
              });
            });

          });

        </script>
      </div>
    </div>
  </div>
</div>
{% endraw %}
```

#### flat nav

To create a nav like the one this site, Next Previous across the tree.
This however only supports 1-2 levels

``` liquid
{%- raw -%}
{% capture string %}{% for p in page.root.menu %}{{ p.url }} {% if p.has_visible_children? %}{% for child in p.visible_children %}{{ child.url }}{% endfor %}{% endif %}{% endfor %}{% endcapture %}

{% assign items = string | split:" " %}

{% for item in items %}
  {% if item == page.url %}

    {% if forloop.first %}
    {% else %}
      {% assign pi = forloop.index0 | minus:1 %}
      {% assign previous = items[pi] %}
    {% endif %}

    {% if forloop.last %}
    {% else %}
      {% assign ni = forloop.index0 | plus:1 %}
      {% assign next = items[ni] %}
    {% endif %}

    {% break %}
  {% endif %}
{% endfor %}

<div id="navigation">
  {% if previous %}
    <a class="nav nav-prev" href="{{ previous }}"> <i class="fa fa-chevron-left"></i></a>
  {% endif %}
  {% if next %}
    <a class="nav nav-next" href="{{ next }}"><i class="fa fa-chevron-right"></i></a>
  {% endif %}
</div>
{% endraw %}
```

#### nav using a recursive loop
This is a simple nav, using a macro for the loop render.

``` liquid
{%- raw -%}
// _nav_side.liquid
<div class="nav-side">
  {% assign nav_loop = page.root.menu %}

  <h3><a href="{{ page.root.url }}">{{ page.root.name }}</a></h3>
  <ul class="nav">
    {% include 'nav_side_loop' %}
  </ul>
</div>
{% endraw %}
```

``` liquid
{%- raw -%}
// _nav_side_loop.liquid
{% for p in nav_loop %}
  {% if p.id == page.id %}
    {% assign current_page = 'active' %}
  {% else %}
    {% assign current_page = '' %}
  {% endif %}

  <li class="{{ current_page }}">
    <a href="{{ p.url }}">
      {% if p.id == page.id %}
        <i class="fa fa-caret-right"></i>
      {% endif %}
      <span>{{ p.name }}</span>
    </a>

    {% assign ancestors = page.ancestors | map: "id" | join: ' '  %}
    {% if p.id == page.id or ancestors contains p.id %}
      {% if p.has_visible_children? %}
        <ul class="nav">
          {% assign nav_loop = p.visible_children %}
          {% include 'nav_side_loop' %}
        </ul>
      {% endif %}
    {% endif %}
  </li>
{% endfor %}
{% endraw %}
```

#### row loop

If you want modulo a different loop then change the `modulo:4` to something else like 2,3,4

``` liquid
{%- raw -%}
// _row_loop.liquid
{% assign count = 1 %}

{% for page in page.root.menu %}
 {% if page.has_visible_children? %}

   {% assign countTop = count | modulo:4 %}
   {% if countTop == 1 %}
     <div class="row">
   {% endif %}

   <div class="col-md-3">
     <h3>{{ page.name }}</h3>
   </div>

   {% assign countBottom = count | modulo:4 %}
   {% if countBottom == 0 %}
     </div>
   {% endif %}

   {% if page.has_visible_children? %}
     {% assign count = count | plus:1 %}
   {% endif %}
 {% endif %}
{% endfor %}

{% assign countEnd = count | modulo:4 %}
{% if countBottom != 1 %}
 </div>
{% endif %}
{% endraw %}
```
result :)

```html
<div class="row">
  <div class="col-md-3"></div>
  <div class="col-md-3"></div>
  <div class="col-md-3"></div>
  <div class="col-md-3"></div>
</div>
<div class="row">
  <div class="col-md-3"></div>
  <div class="col-md-3"></div>
  <div class="col-md-3"></div>
</div>
```

with a regular loop you would get something like this

```html
<div class="row">
  <div class="col-md-3"></div>
  <div class="col-md-3"></div>
  <div class="col-md-3"></div>
  <div class="col-md-3"></div>
  <div class="col-md-3"></div>
  <div class="col-md-3"></div>
  <div class="col-md-3"></div>
</div>
```
