<div>
<ul>
    {% for node in site.pages %}
      {% if node.url contains base_url %}
        {% assign node_url_parts = node.url | split: '/' %}
        {% assign node_url_parts_size = node_url_parts | size %}
        {% assign filename = node_url_parts | last %}
        {% if url_parts_size == node_url_parts_size and filename != 'index.html' %}
          <li><a href='{{node.url}}'>{{node.title}}</a></li>
        {% endif %}
      {% endif %}
    {% endfor %}
    </ul>
</div>