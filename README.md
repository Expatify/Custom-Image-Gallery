# Custom Page with Image Gallery

## Description

Custom Page with Image Gallery Gallery is a touch-enabled, responsive and customizable image gallery and optimized for both mobile and desktop web browsers.
It features swipe, mouse and keyboard navigation, transition effects.

## Setup

Create a new page template `page.image-gallery.liquid`

Add the following section snippet:

`{% section 'image-gallery' %}`

Create a new section liquid `image-gallery.liquid` and copy this codes,

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js" type="text/javascript"></script>

{{ 'rebox.js' | asset_url | script_tag }}
{{ 'rebox.css' | asset_url | stylesheet_tag }}
{{ 'image-gallery.css' | asset_url | stylesheet_tag }}


<div class="gallery-section row">
	<div class="{% if section.settings.container != blank %}{{ section.settings.container }}{% endif %}">
        <div class="content">
            <div class="rows">
                <div class="header text-center">
                    {% if section.settings.description != blank %}
                        <div class="col-xs-12 description">{{section.settings.description }}</div>          
                    {% endif %}
                </div>
            
                {% case section.settings.xs %}
                    {%- when '12' -%}
                        {%- assign xs = 'col-xs-12 ' -%}
                    {%- when '6' -%}
                        {%- assign xs = 'col-xs-6 ' -%}
                    {%- when '4' -%}
                        {%- assign xs = 'col-xs-4 ' -%}
                {% endcase %}

                {% case section.settings.sm %}
                    {%- when '6' -%}
                        {%- assign sm = 'col-sm-6 ' -%}
                    {%- when '4' -%}
                        {%- assign sm = 'col-sm-4 ' -%}
                    {%- when '3' -%}
                        {%- assign sm = 'col-sm-3 ' -%}
                {% endcase %}

                {% case section.settings.md %}
                    {%- when '4' -%}
                        {%- assign md = 'col-md-4 ' -%}
                    {%- when '3' -%}
                        {%- assign md = 'col-md-3 ' -%}
                    {%- when '2' -%}
                        {%- assign md = 'col-md-2 ' -%}
                {% endcase %}

                {% case section.settings.lg %}
                    {%- when '4' -%}
                        {%- assign dimensions = '400x400' -%}
                        {%- assign lg = 'col-lg-4 ' -%}
                    {%- when '3' -%}
                        {%- assign dimensions = '300x300' -%}
                        {%- assign lg = 'col-lg-3 ' -%}
                    {%- when '2' -%}
                        {%- assign dimensions = '200x200' -%}
                        {%- assign lg = 'col-lg-2 ' -%}
                {% endcase %}

                <div id="gallery" class="album">
                    {% for block in section.blocks %}
                        <div class="{{ lg }}{{ md }}{{ sm }}{{ xs }}">
                            <a href="{{ block.settings.image | img_url: 'master' }}" title="{{ block.settings.image.alt }}">
                                <img 
                                    class="thumb img-responsive show-it image-{% increment count %}"
                                    src="{{ block.settings.image | img_url: dimensions, crop: 'center' }}"
                                    alt="{{ block.settings.image.alt }}" />
                            </a>
                        </div>
                    {% endfor %}
                </div>
            </div>
        </div>
	</div>
</div>

<script type="text/javascript">
    $(document).find('#gallery').rebox({ selector: 'a' });
</script>


{% schema %}

    {
        "name": "Image gallery",
        "class": "image-gallery",
        "settings": [
            {
                "type": "richtext",
                "id": "description",
                "label": "Gallery description",
                "default": "<p>Gallery description...</p>"
            },
            {
                "type": "select",
                "id": "xs",
                "label": "Count of images per row on mobile phone.",
                "default": "6",
                "options": [
                    {
                        "value": "12",
                        "label": "One image"
                    }, 
                    {
                        "value": "6",
                        "label": "Two images"
                    }, 
                    {
                        "value": "4",
                        "label": "Three images"
                    } 
                ]
            },
            {
                "type": "select",
                "id": "sm",
                "label": "Count of images per row on tablet.",
                "default": "4",
                "options": [
                    {
                        "value": "6",
                        "label": "Two images"
                    }, 
                    {
                        "value": "4",
                        "label": "Three images"
                    }, 
                    {
                        "value": "3",
                        "label": "Four images"
                    } 
                ]
            },
            {
                "type": "select",
                "id": "md",
                "label": "Count of images per row on laptop.",
                "default": "4",
                "options": [
                    {
                        "value": "4",
                        "label": "Three images"
                    }, 
                    {
                        "value": "3",
                        "label": "Four images"
                    }, 
                    {
                        "value": "2",
                        "label": "Six images"
                    } 
                ]
            },
            {
                "type": "select",
                "id": "lg",
                "label": "Count of images per row on desktop",
                "default": "3",
                "options": [
                    {
                        "value": "4",
                        "label": "Three images"
                    }, 
                    {
                        "value": "3",
                        "label": "Four images"
                    }, 
                    {
                        "value": "2",
                        "label": "Six images"
                    } 
                ]
            }
        ],
        "blocks": [
            {
                "type": "image",
                "name": "Image",
                "settings": [
                    {
                        "type": "image_picker",
                        "id": "image",
                        "label": "Image"
                    }
                ]
            }
        ],
        "presets": [
            {
                "name": "Image gallery",
                "category": "Image Gallery",
                "blocks": [
                    {
                        "type": "image"
                    }
                ]
            }
        ]
    }

{% endschema %}
```

Upload the following javascript & css files to assets folder,

`rebox.js`
`rebox.css`
`image-gallery.css`

## Credits

Developed by Expatify, custom image gallery with rebox jQuery by Trent Richardson - jQuery Rebox [http://trentrichardson.com/examples/jQuery-Rebox]

Learn more https://expatify.co.id/
