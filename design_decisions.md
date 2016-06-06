# Design Decisions

## Simple Integration

The CMS should be very simple to integrate for any website. Furthermore, the CMS should be usable by any technology.

## Refactoring / Type Safety

To have better refactoring tools available, we chose TypeScript which compiles to JavaScript.

## Compilation Pipeline

We want

* to use the latest ES2015 features when programming
* that the code runs in browsers which only support ES5

For these reasons, we use TypeScript (ES6), compile it to JS (ES6), and use babel to compile it so that it works in older browsers (ES5).

## Simplify Publishing

We want to be able to update the CMS without updating each application which uses the CMS.

## Scalability & Performance

We want that the viewing part of the CMS is very scalable and can be used by millions of users. Furthermore, it should be relatively cheap. This is why we use a CDN in front of our API (Amazon Cloudfront) when considering the reading / content loading part.

The editing part doesn't have to be very scalable at the moment. We use an API which is hosted on Heroku and is implemented in Ruby on Rails. This allows the API to be scaled later (add more dynos, add a stronger database).

## Client Performance / Speed / Size

The client part of the Renuo CMS must be slick, since it will be loaded by many clients for viewing. On the other hand, we don't want tor reinvent everything from scratch. Therefore, we follow the following strategy:

* We require a jQuery-like interface, especially for the AJAX requests. This must be included before the Renuo CMS
* We load the CKEDITOR dynamically from a CDN only when it is needed for editing.

## Frontend vs. Backend

We want to split up the frontend and backend, so that we can use the technologies we believe fit together well. The interface between the two parts are documented by [Swagger](http://petstore.swagger.io/?url=https://renuo-cms-api-develop.herokuapp.com/swagger.yml).

## In-place Editor

We want to be able to edit the content in-place for simplicity reasons.

## Editor and Data Format

The data format should be arbitrary considering the API / data storage. On the client, we currently use HTML as data format. In the future, we may also support other formats like markdown.

In an ideal world there would be a simple WYSIWYG editor which is stable and produces markdown output. However, after long discussions, we decided to use a WYSIWYG editor - namely CKEDITOR. We use the [Advanced Content Filter](http://sdk.ckeditor.com/samples/acf.html) to filter out invalid HTML tags. We are very strict on which tags can be used, and the goal is that we can switch between WYSIWYG editors freely.

## File Upload

For features like uploading images and use them on the web page, an upload service is needed. We decided to make use of the [Renuo-Upload](https://renuo.gitbooks.io/renuo-upload-doc/content/index.html) which is a service that we developed before.

## Conclusion

For all these reason, we use a JavaScript script which loads the CMS. This script is hosted on a CDN and will be updated without updating the application itself. The data is stored on a central CMS API server (implemented using Rails API). Furthermore, a CDN is used to deliver content, but not to edit content.