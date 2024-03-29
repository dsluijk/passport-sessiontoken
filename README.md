# passport-sessiontoken

A [Passport](https://github.com/jaredhanson/passport) strategy based on [passport-localapikey](https://github.com/cholalabs/passport-localapikey).

## What changed?
 - Now also looks in headers for the token.
 - Custom token title

## Installation
    $ npm install passport-sessiontoken
    
## Usage
### Define Strategy
    passport.use(new SessionStrategy(
        function(apikey, done) {
            User.findOne({ apikey: apikey }, function (err, user) {
                if (err) { return done(err); }
                if (!user) { return done(null, false); }
                return done(null, user);
            });
        }, {header: 'customHeader', field: 'customField'}
    ));
    
### Authenticate in request
    app.post('/api/authenticate', 
        passport.authenticate('sessiontoken', { session: false,failureRedirect: '/api/unauthorized' }),
        function(req, res) {
            res.json({ message: "Authenticated" })
        }
    );
    
## Default fields
 - header: x-token
 - Body & Query: token
    
## Field order
 - Header
 - Body
 - Query (Not recommented)
    
## Credits
 - [AtlasDev](https://www.atlasdev.nl)

## Licence
The MIT License (MIT)

Copyright (c) 2015 Dany Sluijk

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
