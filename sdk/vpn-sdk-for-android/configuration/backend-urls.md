# Backend urls

By default SDK uses multiple urls for backend api calls and fallback to different url when some error happen.

First it uses urls passed to **ClientInfo#addUrls** and **ClientInfo#addUrl**

Then default urls integrated to the sdk

To override these default urls add new **raw** resource to your project with name **pango\_default\_urls.json**

Follow the structure

```
{  
    "primary": [    
        "https://url-1.net",    
        "https://url-2.com",    
        "https://url-3.com"  
    ]
}
```

You can change the urls or specify **primary** array as empty to keep only ClientInfo urls
