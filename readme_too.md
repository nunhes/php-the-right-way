Vexo que queres traducir o proxecto "PHP: The Right Way" ao galego! Este é un proxecto moi importante para a comunidade PHP que proporciona boas prácticas e información de calidade para desenvolvedores PHP.

Vou explorar a estrutura do proxecto para entender mellor como está organizado e como poderías contribuír coa tradución ao galego.

Ran tool
Ran tool
Read file: CONTRIBUTING.md
Read file: _config.yml
Read file: _posts/01-01-01-Getting-Started.md
Read file: _posts/01-02-01-Use-the-Current-Stable-Version.md
Perfecto! Agora entendo a estrutura do proxecto. "PHP: The Right Way" é unha guía completa de boas prácticas para PHP que está organizada como un sitio web Jekyll. Vou explicarte como poderías contribuír coa tradución ao galego:

## Estrutura do Proxecto

O proxecto está organizado da seguinte maneira:

1. **Contido principal**: Os artigos están en `_posts/` con nomes como `01-02-01-Use-the-Current-Stable-Version.md`
2. **Configuración**: `_config.yml` define a configuración do sitio
3. **Navegación**: A estrutura de navegación xérase automaticamente baseada nos arquivos de `_posts/`

## Como Contribuír coa Tradución ao Galego

Segundo o README, hai dúas opcións para traducións:

### Opción 1: Fork con GitHub Pages
1. **Facer fork** do repositorio principal
2. **Traducir** todo o contido ao galego
3. **Publicar** no teu propio GitHub Pages como `[username].github.io/php-the-right-way`

### Opción 2: Subdominio
1. **Facer fork** do repositorio
2. **Traducir** todo o contido
3. **Configurar** un subdominio como `gl.phptherightway.com`
4. **Solicitar** configuración DNS aos mantenedores

## Pasos Recomendados

1. **Facer fork** do repositorio:
   ```bash
   git clone https://github.com/codeguy/php-the-right-way.git
   ```

2. **Instalar dependencias** para previsualizar localmente:
   ```bash
   bundle install --path vendor/bundle
   bundle exec jekyll serve
   ```

3. **Traducir os arquivos** en `_posts/` ao galego, mantendo:
   - A estrutura de front matter (YAML no inicio)
   - Os enlaces e referencias
   - O formato Markdown
   - Os exemplos de código (non traducir)

4. **Actualizar** `_config.yml` co título e descrición en galego

5. **Crear** un README.md en galego explicando a tradución

## Exemplo de Tradución

Aquí tes un exemplo de como traducir un dos arquivos:

**Orixinal (inglés):**
```markdown
---
title:   Use the Current Stable Version (8.4)
isChild: true
anchor:  use_the_current_stable_version
---

## Use the Current Stable Version (8.4) {#use_the_current_stable_version_title}

If you are getting started with PHP, start with the current stable release of [PHP 8.4][php-release]...
```

**Tradución (galego):**
```markdown
---
title:   Usa a Versión Estable Actual (8.4)
isChild: true
anchor:  use_the_current_stable_version
---

## Usa a Versión Estable Actual (8.4) {#use_the_current_stable_version_title}

Se estás a comezar con PHP, comeza coa versión estable actual de [PHP 8.4][php-release]...
```

## Recursos Adicionais

- **Guía de estilo**: Seguir as regras do `CONTRIBUTING.md`
- **Formato**: Usar 4 espazos para indentación, 120 caracteres por liña
- **Código**: Manter os exemplos de código en inglés
- **Enlaces**: Manter as URLs orixinais

