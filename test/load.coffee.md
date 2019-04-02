    (require 'chai').should()
    describe 'The module', ->
      it 'should load', ->
        require '..'
      it 'should return a function', ->
        (require '..').should.be.a 'function'
      it 'should compute an object', ->
        m = require '..'
        r = m 'https://dud%40for:u%20o@127.0.0.1:5984', 'something'
        r.should.have.property 'url', 'https://127.0.0.1:5984/something',
        r.should.have.property 'headers'
        r.headers.should.have.property 'Authorization', 'Basic ZHVkQGZvcjp1IG8='
