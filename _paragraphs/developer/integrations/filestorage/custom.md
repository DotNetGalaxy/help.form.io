---
title: Custom Url
book: developer
section: integrations
chapter: filestorage
slug: url
weight: 100
---
Custom Url Provider does not have any settings in the Project Settings. Instead, it is set in the *Url* field on the form component when it is added to a form.

In order to use a Custom Url Provider, you will need to set up a service that can upload and serve files. See [https://github.com/danialfarid/ng-file-upload#server-side](https://github.com/danialfarid/ng-file-upload#server-side) for setting up a compatible service.

The information posted to the server will be 

```
{
  file: file
}
```

The server should save the contents of the file somewhere and return the following object.

```
{
  url: 'http://link.to/file',
  name: 'The_Name_Of_The_File.doc',
  size: 1000
}
```

You may return additional attributes if desired.