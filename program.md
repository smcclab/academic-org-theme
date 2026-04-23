---
layout: page  
title: Program
permalink: /program/
---

{% assign sorted_sessions = site.data.sessions | sort: "start" %}

<script>
  var calendarEvents = (function () {
    var sessions = {{ sorted_sessions | jsonify }};
    var typeColours = {
      admin:      '#2e312d',
      keynote:    '#b69255',
      papers:     '#7e7a72',
      artworks:   '#565b68',
      workshops:  '#5f6e62',
      discussion: '#97a7b6'
    };
    return sessions.map(function (session) {
      var colour = typeColours[session.type];
      return Object.assign({}, session, {
        url: '{{ site.baseurl }}/sessions/' + session.id + '.html',
        backgroundColor: colour,
        borderColor: colour
      });
    });
  })();
</script>

{% include calendar-timezone-picker.html
   default_timezone="Australia/Sydney"
   default_timezone_label="Sydney (Default)" %}

<h2>Sessions</h2>


<div class="row row-cols-1 row-cols-md-2 g-4">
  {% for session in sorted_sessions %}
    {% capture session_url %}{{ session.id | datapage_url: "sessions" | relative_url }}{% endcapture %}
    <div class="col">
      <div class="card h-100">
        {% if session.image_url %}
          <img src="{{ session.image_url | relative_url }}" class="card-img-top" alt="{{ session.title }}">
        {% endif %}
        <div class="card-body">
          <h5 class="card-title">
            <a href="{{ session_url }}" class="text-decoration-none text-dark">{{ session.title }}</a>
          </h5>
          <h6 class="card-subtitle mb-2 text-muted">{{ session.type | capitalize }} Session</h6>
          <p class="card-text">
            <strong>Date:</strong> {{ session.date | date: "%A, %B %d, %Y" }}<br>
            <strong>Time:</strong> {{ session.date | date: "%I:%M %p" }}<br>
            <strong>Location:</strong> {{ session.location }}<br>
            <strong>Chair:</strong> {{ session.chair }}
          </p>
        </div>
        <div class="card-footer">
          <a href="{{ session_url }}" class="btn btn-outline-secondary">Details</a>
          {% if session.video_url %}
            <a href="{{ session.video_url }}" class="btn btn-outline-secondary" target="_blank">Video</a>
          {% endif %}
        </div>
      </div>
    </div>
  {% endfor %}
</div>
