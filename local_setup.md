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

log in to amazon if you aren't already cause you just set up your s3 bucket

navigate to IAM -> click on Identity & Access Management

navigate to Users in the navigation on the left side

click on the blue button with white writing in the form of "create user"

enter your name into the first field

press "create" which you'll find in the lower right corner its blue with white writing

click on "Show User Security Credentials" and you see your needed keys yeyy!! now you learn them by heart, as you'll need them afterwards and because its a good training for your brain. you should do stuff like that several times a day to keep your brain fit.

### Configure renuo-upload-signing

Now you have to use the newly created bucket in your renuo-upload-signing. the S3_BUCKET_NAME needs the name you gave to your bucket when you set up you amazon S3 bucket. the CDN_HOST differs if you changed the location for example. the part behind the "/" will always be your bucket-name though. The S3_PUBLIC_KEY needs the "Access Key ID" which is the one you learned by heart before. Else you'll find it in the IAM of your amazon account. the same is with the S3_SECRET_KEY which is the "Secret Access Key".

```rb
S3_BUCKET_NAME: 'renuo-upload-<yourname>-development'
S3_PUBLIC_KEY: 'your public key found in Amazon IAM'
S3_SECRET_KEY: 'your secret key found in Amazon IAM'
CDN_HOST: 's3.eu-central-1.amazonaws.com/renuo-upload-<yourname>-development' #without https://, just the domain
```

### Set Up renuo-cms-demo as example project

clone it to your local machine

```
git clone git@github.com:renuo/renuo-cms-demo.git
```

set up renuo cms to manage content blocks for the page

```rb
CredentialPair.create(
 private_api_key: "47DTrw46jNDtt53g56Hg5MMt5",
 api_key: "T3i1A247Rd1",
 project_name: "renuo-cms-demo",
 renuo_upload_api_key: "apiKeyOfRenuoUpload",
 renuo_upload_signing_url: "urlOfRenuoUploadSigning/generate_policy"
)
```
