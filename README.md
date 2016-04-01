# Parse-Server-Azure
<a href="https://www.npmjs.com/package/parse-server-azure"><img src="https://badge.fury.io/js/parse-server-azure.svg" alt="npm version" height="18"></a> <a href="https://david-dm.org/felixrieseberg/parse-server-azure"><img src="https://david-dm.org/felixrieseberg/parse-server-azure.svg" alt="dependencies" height="18px"></a> Adapters, tools, and documentation to use Parse-Server with Microsoft Azure, brought to you by your friends at Microsoft.

> :memo: Find detailed instructions in the [Wiki](https://github.com/felixrieseberg/parse-server-azure/wiki)!

```
npm install parse-server-azure
```

If you're using `parse-server` at version 2.2 (or below), please install with:

```
npm install parse-server-azure-storage@0.1.2
```


## FilesAdapter
By default, Parse-Server uses the `GridStoreAdapter` to store files, meaning that files will be stored in the connected database. For better performance, you can store files in Azure Blob Storage, using this module's `FilesAdapter`.

```js
var ParseServer         = require('parse-server').ParseServer;
var AzureStorageAdapter = require('parse-server-azure').FilesAdapter;

var account = 'YOUR_AZURE_STORAGE_ACCOUNT_NAME';
var container = 'YOUR_AZURE_STORAGE_CONTAINER_NAME';
var options = {
    accessKey: 'YOUR_ACCESS_KEY',
    directAccess: false // If set to true, files will be served by Azure Blob Storage directly
}

var api = new ParseServer({
  appId: process.env.APP_ID || 'myAppId',
  serverURL: process.env.SERVER_URL || 'http://localhost:1337'
  (...)
  filesAdapter: new AzureStorageAdapter(account, container, options);
});
```

#### Direct Access
By default, Parse will proxy all files - meaning that your end user accesses the files via your open source Parse-Server, not directly by going to Azure Blob storage. This is useful if you want files to only be accessible for logged in users or have otherwise security considerations.

If your files can be public, you'll win performance by accessing files directly on Azure Blob Storage. To enable, ensure that your container's security policy is set to `blob`. Then, in your adapter options, set `directAccess: true`.

## License
The MIT License (MIT); Copyright (c) 2016 Microsoft Corporation. Please see `LICENSE` for details.
