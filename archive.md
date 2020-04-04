---
layout: default
permalink: /archive
---

<main>

<div class="Any-horInsets">

<div class="ArchiveHeader">
	<h1>Articles</h1>
</div>

{% for post in site.posts  %}
    {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
    {% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}

    {% if forloop.first %}
    <h2 class="SectionTitle" id="{{ this_year }}-ref">{{this_year}}</h2>
    <ul class="ArchivePostList">
    {% endif %}

	{% include archive-post-list-item.html %}

    {% if forloop.last %}
    </ul>
    {% else %}
        {% if this_year != next_year %}
        </ul>
        <h2 class="SectionTitle" id="{{ next_year }}-ref">{{next_year}}</h2>
        <ul class="ArchivePostList">
        {% endif %}
    {% endif %}
{% endfor %}

</div> <!--home!-->

</main>
