# Contract: Figure Include

**Type**: Template include contract
**File**: `_includes/figure.html`

---

## Usage

```liquid
{% include figure.html
   src="/assets/images/example.png"
   alt="Description of the image"
   caption="Figure 1: What this shows"
   source_name="Author Name"
   source_url="https://example.com/original-post" %}
```

## Parameters

| Parameter | Required | Type | Description |
|-----------|----------|------|-------------|
| `src` | Yes | String | Image path or URL |
| `alt` | Yes | String | Alt text (accessibility) |
| `caption` | No | String | Visible caption below image |
| `source_name` | No | String | Original author or publication name |
| `source_url` | No | String | URL to original source |

## Rendered HTML Structure

```html
<figure class="post-figure">
  <img src="{src}" alt="{alt}">
  <figcaption>
    <span class="caption">{caption}</span>          <!-- omitted if no caption -->
    <span class="attribution">
      Source: <a href="{source_url}">{source_name}</a>  <!-- linked if both present -->
      <!-- plain text if source_name only, URL if source_url only, "Source unknown" if neither -->
    </span>
  </figcaption>
</figure>
```

## Fallback Behaviour

| Scenario | Output |
|----------|--------|
| Both `source_name` and `source_url` present | `Source: <a href="{url}">{name}</a>` |
| `source_name` only | `Source: {name}` (plain text) |
| `source_url` only | `Source: <a href="{url}">{url}</a>` |
| Neither present | `Source: unknown` |
| No `caption` | `<figcaption>` contains only attribution span |
| No `caption` and no attribution | No `<figcaption>` rendered |
