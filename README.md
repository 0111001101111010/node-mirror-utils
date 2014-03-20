NodeJS Mirror API Utils
==========================

This is a helper utility library for the Google Glass Mirror API. Here is how to use it with express:

    app.get('/install', authUtils.install);
    app.get('/oauth2callback', function(req, res){
        // if we're able to grab the token, redirect the user back to the main page
        authUtils.getToken(req.query.code, function(data) {
            console.log('failure',data);
            res.end();
        }, function(oauth2Client, client) {
            console.log('success',oauth2Client, client);
            var timelineUtils = new mirror.Timeline(oauth2Client, client);
            var menu = menuUtils.buildSimpleDefault().build();
            var card = cardUtils.reset().id(123).title("test").text("hello").menus(menu).build();
            console.log('try to insert card',card);
            timelineUtils.insertCard(card, failure, success);
            res.end();
        });
    });

More documentation to come.

This is a work in progress.
