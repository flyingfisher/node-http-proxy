forked from <a href="https://github.com/nodejitsu/node-http-proxy">nodejitsu/node-http-proxy</a>

Add ability to change response script and link relative url when proxy

Add this ability for meteor in this moment 
(version 0.6.4 still not support ROOT_URL, so I change proxy code to avoid this problem)

normal usage:
```js
var httpProxy = require('seafish-http-proxy-meteor');

var options = {
  replaceRelativePath: true,
  pathnameOnly: true,
  router: {
    '/wiki': '127.0.0.1:8001',
    '/blog': '127.0.0.1:8002/blog',
    '/api':  '127.0.0.1:8003'
  }
}

var proxyServer = httpProxy.createServer(options);
proxyServer.listen(80);
```

meteor usage: before 0.6.6.1
```js
var httpProxy = require('seafish-http-proxy-meteor');

var options = {
  replaceRelativePath: true,
  pathnameOnly: true,
  router: {
    '/meteor': '127.0.0.1:3000',
    '/sockjs': '127.0.0.1:3000/sockjs',
    '/otherapp': '127.0.0.1:8002'
  }
}

var proxyServer = httpProxy.createServer(options);
proxyServer.listen(80);
```

meteor usage: after 0.6.6.1
```js
// suppose ROOT_URL is "localhost:3000/meteor"
var httpProxy = require('seafish-http-proxy-meteor');

var options = {
  pathnameOnly: true,
  router: {
    '/meteor': '127.0.0.1:3000/meteor',
    '/otherapp': '127.0.0.1:8002'
  }
}

var proxyServer = httpProxy.createServer(options);
proxyServer.listen(80);
```

Simple use
```js
// suppose ROOT_URL is "localhost:3000"
var httpProxy = require('seafish-http-proxy-meteor');

var options = {
  pathnameOnly: true,
  router: {
    '/otherapp': '127.0.0.1:8002',
    '/': '127.0.0.1:3000/',
  }
}

var proxyServer = httpProxy.createServer(options);
proxyServer.listen(80);
```

Use with https
```js
// suppose ROOT_URL is "localhost:3000"
var httpProxy = require('seafish-http-proxy-meteor');

var options = {
  pathnameOnly: true,
  router: {
    '/otherapp': '127.0.0.1:8002',
    '/': '127.0.0.1:3000/',
  },
  https: {
    key: "",
    cert: ""
  }
}

var proxyServer = httpProxy.createServer(options);
proxyServer.listen(443);
```

The replaceRelativePath option, work for html page, change things like 
```html
<script src="/test.js"></script>
``` 
into
```html
<script src="/path/test.js"></script>
```
