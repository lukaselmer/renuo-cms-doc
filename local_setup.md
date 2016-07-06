# Local Setup

For developing you want to set up the renuo-cms and the renuo-upload locally. They must be set up once and can then be used by every application that uses one or both of those services.

## Step by Step Manual

### Install renuo-cms-api

Clone git repository and run bin/setup:

```
git clone git@github.com:renuo/renuo-cms-api.git
cd renuo-cms-api
bin/setup
```

If you already cloned the project, you can just pull the newest version and migrate the database.

### Install renuo-upload signing

Follow the instructions on:<br>
https://renuo.gitbooks.io/renuo-upload-doc/content/local_setup.html

### Set Up renuo-cms-demo as Example Project (optional)

1.  Clone it to your local machine:
```
git clone git@github.com:renuo/renuo-cms-demo.git
```
1.  Configure it in renuo-upload-signing by adding this line to the file ```config/.env```. For this you have to generate a key:
```rb
API_KEYS: {"key":"<generated-key>","app_name":"renuo-cms-demo","env": "development"}
```

1.  Configure it in renuo-cms-api. Open the console with ```rails c``` and write:

  ```rb
CredentialPair.create(
 private_api_key: "47DTrw46jNDtt53g56Hg5MMt5",
 api_key: "T3i1A247Rd1",
 project_name: "renuo-cms-demo",
 renuo_upload_api_key: "<generated-key>",
 renuo_upload_signing_url: "http://renuo-upload-signing.dev:3003/generate_policy"
)
```
Replace ```<generated-key>``` with the key you generated and used in the renuo-upload-signing.

1.  Navigate to the ```index.html``` of renuo-cms-demo and make a search/replace with:

  -  search for ```https://renuo-cms-api-demo.herokuapp.com/``` 
  -  replace with: ```//renuo-cms-api.dev:3002```

### Run All Applications

1.  Run renuo-upload-signing
```
bin/run
```

1.  Run renuo-cms-api
```
bin/run
```

1.  Run renuo-cms-demo. You can also run it with any server you like, as it is a static page. This is just an example:
```
cd page1
npm install http-server -g
http-server . -a renuo-cms-demo.dev
```
For making this work add the line: ```127.0.0.1 renuo-cms-demo.dev``` to your ```/etc/hosts``` file.
