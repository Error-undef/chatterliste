---
layout: liste
---
<div class="buttons">
  <a href="https://github.com/denog/chatterliste/issues/new/choose" class="button" target="_blank">Daten anlegen oder ändern</a>
</div>
<table>
  <thead>
    <tr>
      <th>Nick</th>
      <th>Name</th>
      <th>NIC-Handle</th>
      <th>ASN</th>
      <th>Organisation</th>
    </tr>
  </thead>
  <tbody>
  {% assign sorted = site.data.chatterliste | sort_natural: 'Nick' %}
  {% for entry in sorted %}
    <tr>
      <td>{{ entry.Nick }}</td>
      <td>{{ entry.Name }}</td>
      <td>
        {% if entry["NIC Handle"] %}{% for handle in entry["NIC Handle"] %}
        <a href="https://apps.db.ripe.net/db-web-ui/query?searchtext={{ handle }}&flags=r&types=PERSON" target="_blank">{{ handle }}</a><br>
        {% endfor %}{% endif %}
      </td>
      <td>
        {% if entry.ASN %}{% for asn in entry.ASN %}
          <a href="https://apps.db.ripe.net/db-web-ui/query?searchtext=AS{{ asn }}&flags=r&types=AUT_NUM" target="_blank">{{ asn }}</a><br>
        {% endfor %}{% endif %}
      </td>
      <td>
        {% if entry.Organisation %}{% for org in entry.Organisation %}
          {% if org.url %}<a href="{{ org.url }}" target="_blank">{% endif %}
          {{ org.name }}
          {% if org.url %}</a>{% endif %}
          <br>
        {% endfor %}{% endif %}
      </td>
    </tr>
  {% endfor %}
  </tbody>
</table>
