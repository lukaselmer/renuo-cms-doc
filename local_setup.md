# Local Setup

For developing you want to set up the renuo-cms and the renuo-upload locally. It must be set up once and can then be used by every application that uses the renuo-cms or the renuo-upload.

## Step by Step manual

### Install renuo-cms-api

Clone git repositiory and run bin/setup:
```
git clone git@github.com:renuo/renuo-cms-api.git
cd renuo-cms-api
bin/setup
```

### Install renuo-upload signing
Clone git repository and run bin/setup:
```
git clone git@github.com:renuo/renuo-upload-signing.git
cd renuo-upload-signing
bin/setup
```

### Set Up a Amazon S3 bucket

sign in to amazon

navigate to s3 -> click on s3 icon

create new bucket -> click on blue button on top with text "create bucket"

give it a name, we request to do something like renuo-upload-<yourname>-development, but you can choose whatever you want. and choose to place where your server should be. we usually use frankfurt.

click on your project and navigate to Properties (right side of navigation). click on the Permission section to fold it out and click on the butten called "Add CORS Configuration".
Insert this:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
    <CORSRule>
        <AllowedOrigin>*</AllowedOrigin>
        <AllowedMethod>GET</AllowedMethod>
        <AllowedMethod>POST</AllowedMethod>
        <MaxAgeSeconds>3000</MaxAgeSeconds>
        <AllowedHeader>*</AllowedHeader>
    </CORSRule>
</CORSConfiguration>
```
and click on save, then on close and then on the blue save again

### Set UP Amazon IAM


