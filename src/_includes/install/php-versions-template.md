支持的PHP版本:

{% for version in supported_php_versions %}

{% if version != '~7.1.3' %}

*  {{ version }}

{% endif %}

{% endfor %}
