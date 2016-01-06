# Usage

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/renuo-cms-client/latest/renuo-cms-client.min.js"></script>
```

Insert a ```<div>``` element with the data attribute block containing the content block path:

```html
<div data-content-path="some/path/to/some/content" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey"></div>
```

If you want to be able to edit the content block (only the admin should have this!):

```html
<div data-content-path="some/path/to/some/content" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey" data-private-api-key="AdminONLY"></div>
```

The library will automagically initialize and manage the content blocks. If you want to reload the content blocks, you can use the following trigger:

```js
jQuery(document).trigger('renuo-cms-reload');
```

## Default content and paragaraphs in contents

The wysiwyg editor by default automatically inserts a ```<p>``` (paragraph) when editing content. In most cases this makes sense, since the edited text is semantically split into paragraphs. However, for certain blocks you don't want that the editable content is automatically wrapped in a paragraph. Consider the following example (including the solution):

```html
<!-- By default, if no default content is set, paragraphs are enabled. -->
<div data-content-path="li-element" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey" data-private-api-key="AdminONLY"></div>

<ul class="special-ul">
  <li class="special-li">
    <div data-content-path="li-element" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey" data-private-api-key="AdminONLY">
      If no paragraphs are present in the default content, then paragraphs are disabled.
    </div>
  </li>
</ul>

<div data-content-path="li-element" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey" data-private-api-key="AdminONLY">
  <p>When paragraphs are present in the default content, then paragraphs are enabled.</p>
</div>
```

We also considered the following, but currently we don't see a reason to implement it.

```html
<!-- This is not implemented --><div data-not-implemented-content-paragraphs="true" data-content-path="li-element" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey" data-private-api-key="AdminONLY">
  <h1>You can also manually enable paragraphs using the data-content-paragraphs="true" config.</h1>
</div>

<!-- This is not implemented --><div data-not-implemented-content-paragraphs="false" data-content-path="li-element" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey" data-private-api-key="AdminONLY">
  <p>You can also manually disable paragraphs using the data-content-paragraphs="false" config.</p>
</div>
```