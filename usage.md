# Usage

Set up your renuo-cms-api for your project:
```rb
CredentialPair.create(
 private_api_key: "AdminONLY",
 api_key: "aValidApiKey",
 project_name: "some-project",
 renuo_upload_api_key: "apiKeyOfRenuoUpload",
 renuo_upload_signing_url: "urlOfRenuoUploadSigning/generate_policy"
)
```

Require renuo-cms-client in your html:
```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/renuo-cms-client/latest/renuo-cms-client.min.js"></script>
```

Insert a ```<div>``` element with the data attribute block containing the content block path. In the following examples, ```"//renuo-cms-api.dev:3000"``` is a placeholder for the URL your renuo-cms-api runs on:

```html
<div data-content-path="some/path/to/some/content" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey"></div>
```

If you want to be able to edit the content block (only admins should have permissions to do so!):

```html
<div data-content-path="some/path/to/some/content" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey" data-private-api-key="AdminONLY"></div>
```

The library will automatically initialize and manage the content blocks. If you want to reload the content blocks, you can use the following trigger:

```js
jQuery(document).trigger('renuo-cms-reload');
```

## Image-/File-Upload
As soon as you set the following keys in you renuo-cms-api for your project, you can upload images with the editor:
```rb
renuo_upload_api_key: "apiKeyOfRenuoUpload",
renuo_upload_signing_url: "urlOfRenuoUploadSigning/generate_policy"
```

## Default content and paragaraphs in contents

By default, the wysiwyg editor automatically inserts a ```<p>``` (paragraph) while the content is edited. In most cases this makes sense, since the edited text is semantically split into paragraphs. However, for certain blocks you don't want that the editable content is automatically wrapped in a paragraph. Consider the following example (including the solution):

```html
<!-- By default, if no default content is set, paragraphs are enabled. -->
<div data-content-path="li-element" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey" data-private-api-key="AdminONLY"></div>

<ul class="special-ul">
  <li class="special-li">
    <div data-content-path="li-element" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey" data-private-api-key="AdminONLY">
      Paragraphs are disabled if no paragraphs are present in the default content.
    </div>
  </li>
</ul>

<div data-content-path="li-element" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey" data-private-api-key="AdminONLY">
  <p>Paragraphs are enabled if paragraphs are present in the default content.</p>
</div>
```

We also considered the following way to override the automatic detection, but currently we don't see a reason to implement it.

```html
<!-- This is not implemented --><div data-not-implemented-content-paragraphs="true" data-content-path="li-element" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey" data-private-api-key="AdminONLY">
  <h1>You can also manually enable paragraphs using the data-content-paragraphs="true" config.</h1>
</div>

<!-- This is not implemented --><div data-not-implemented-content-paragraphs="false" data-content-path="li-element" data-api-host="//renuo-cms-api.dev:3000" data-api-key="aValidApiKey" data-private-api-key="AdminONLY">
  <p>You can also manually disable paragraphs using the data-content-paragraphs="false" config.</p>
</div>
```

## renuo-cms with rails


The gem [renuo-cms-rails](https://github.com/renuo/renuo-cms-rails) provides simpler usage of the renuo-cms if you use it with rails.

## Installation

In case you want to use the renuo-cms and you don't have access to a running renuo-cms already, you need to set up the following web-services. The documentation on how to install each of them can be found on GitHub. The links billow will lead you to the projects on GitHub.

* [renuo-cms-client](https://github.com/renuo/renuo-cms-client)
* [renuo-cms-api](https://github.com/renuo/renuo-cms-api)

If you want the upload feature, following services are needed additionally:

* [renuo-upload](https://github.com/renuo/renuo-upload)
* [renuo-upload-signing](https://github.com/renuo/renuo-upload-signing)
* [renuo-thumbs-proxy](https://github.com/renuo/renuo-thumbs-proxy)
* [renuo-thumbor](https://github.com/renuo/renuo-thumbor)
* [Amazon Cloudfront-Service](https://aws.amazon.com/cloudfront/)
* [Amazon s3 bucket](https://aws.amazon.com/s3/)
* [AWS Identity and Access Management (IAM)](https://aws.amazon.com/de/iam/)

Read more about the [renuo-upload](https://renuo.gitbooks.io/renuo-upload-doc/content/index.html).

