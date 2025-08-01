---
title: "Plataformas CTF"
layout: single
permalink: /platforms/
author_profile: true
classes: wide
---

<style>
.platforms-container {
  max-width: 1200px;
  margin: 2rem auto;
}

.platforms-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.platform-card {
  background: var(--background-color, #fff);
  border: 1px solid var(--border-color, #e1e4e8);
  border-radius: 12px;
  padding: 2rem;
  text-align: center;
  transition: all 0.3s ease;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.platform-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 25px rgba(0,0,0,0.15);
}

.platform-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.platform-name {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
  color: var(--text-color, #24292e);
}

.platform-description {
  color: var(--muted-text-color, #586069);
  margin-bottom: 1.5rem;
  font-size: 0.95rem;
}

.platform-stats {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
  font-size: 0.9rem;
}

.posts-count {
  background: var(--primary-color, #007cba);
  color: white;
  padding: 0.25rem 0.75rem;
  border-radius: 12px;
  font-weight: bold;
}

.visit-platform {
  color: var(--link-color, #0366d6);
  text-decoration: none;
  font-weight: 500;
}

.visit-platform:hover {
  text-decoration: underline;
}

.platform-posts {
  border-top: 1px solid var(--border-color, #e1e4e8);
  padding-top: 1rem;
  text-align: left;
}

.platform-posts h4 {
  font-size: 1rem;
  margin-bottom: 0.75rem;
  color: var(--text-color, #24292e);
}

.platform-posts ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.platform-posts li {
  margin-bottom: 0.5rem;
}

.platform-posts a {
  color: var(--link-color, #0366d6);
  text-decoration: none;
  font-size: 0.9rem;
}

.platform-posts a:hover {
  text-decoration: underline;
}

.view-all {
  display: inline-block;
  margin-top: 0.5rem;
  color: var(--success-color, #28a745);
  font-weight: 500;
  text-decoration: none;
  font-size: 0.9rem;
}

.view-all:hover {
  text-decoration: underline;
}

.coming-soon {
  color: var(--muted-text-color, #586069);
  font-style: italic;
  border-top: 1px solid var(--border-color, #e1e4e8);
  padding-top: 1rem;
}

@media (max-width: 768px) {
  .platforms-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .platform-card {
    padding: 1.5rem;
  }
  
  .platform-stats {
    flex-direction: column;
    gap: 0.5rem;
  }
}
</style>

<div class="platforms-container">
  <h1 style="text-align: center; margin-bottom: 1rem;">🎯 Plataformas de Práctica CTF</h1>
  <p style="text-align: center; color: var(--muted-text-color, #586069); margin-bottom: 2rem;">
    Explora writeups y guías de las principales plataformas de ciberseguridad
  </p>
  
  <div class="platforms-grid">
    {% for platform in site.data.platforms %}
      <div class="platform-card">
        <div class="platform-icon" style="color: {{ platform.color }}">
          <i class="{{ platform.icon }}"></i>
        </div>
        <h2 class="platform-name">{{ platform.name }}</h2>
        <p class="platform-description">{{ platform.description }}</p>
        
        <!-- Contar posts por plataforma -->
        {% assign platform_posts = site.posts | where_exp: "post", "post.categories contains platform.slug" %}
        {% assign posts_count = platform_posts.size %}
        
        <div class="platform-stats">
          <span class="posts-count">{{ posts_count }} writeups</span>
          <a href="{{ platform.website }}" target="_blank" class="visit-platform">
            Visitar sitio <i class="fas fa-external-link-alt"></i>
          </a>
        </div>
        
        <!-- Mostrar posts si existen -->
        {% if posts_count > 0 %}
          <div class="platform-posts">
            <h4><i class="fas fa-file-alt"></i> Últimos writeups:</h4>
            <ul>
              {% for post in platform_posts limit:3 %}
                <li>
                  <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
                  <small style="color: var(--muted-text-color, #586069);">
                    - {{ post.date | date: "%b %Y" }}
                  </small>
                </li>
              {% endfor %}
            </ul>
            {% if posts_count > 3 %}
              <a href="/categories/#{{ platform.slug }}" class="view-all">
                Ver todos los {{ posts_count }} writeups →
              </a>
            {% endif %}
          </div>
        {% else %}
          <div class="coming-soon">
            <i class="fas fa-clock"></i> Próximamente...
          </div>
        {% endif %}
      </div>
    {% endfor %}
  </div>
</div>