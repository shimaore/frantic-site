    URL = require 'url'
    module.exports = (base,name) ->
      site = URL.parse base
      ref = {}
      ref.url = URL.format
        protocol: site.protocol
        host: site.host
        pathname: name

...even with CouchDB ~~1.6.1~~ 2.1.1 we still have the issue with CouchDB not properly managing authorization headers when a username and password are provided in the original URI that contains "special" characters (like `@` or space). So let's handle it ourselves.

      if site.auth?
        auth = (Buffer.from site.auth).toString 'base64'
        ref.headers =
          Authorization: "Basic #{auth}"
      ref
