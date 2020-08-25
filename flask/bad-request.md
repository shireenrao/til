# Bad Request Version

Once I start my server on localhost and access the page on a browser, I saw this error

```
127.0.0.1 - - [24/Aug/2020 15:43:21] code 400, message Bad request version ('localhost\x00\x17\x00\x00ÿ\x01\x00\x01\x00\x00')
```

Just make sure your url is http and not https. DUH!
