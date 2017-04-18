# OAuth Redirect Bounce

App developers can use oauth.click as an OAuth 2.0 callback redirect URL for custom schemes.

## Why?

You write a mobile app that's an OAuth 2.0 client. The authorization server requires the callback URL to your client to start with "https://". Your app doesn't receive requests on https, but instead on foo:// (or something else non-standard). This listens on https for you and redirects to any custom scheme you like.

## Any scheme? How about another https or http server?

No. Since this is intended only to be used by apps that require custom schemes, it will not redirect to schemes used by traditional web browsers.

## How do I use it?

Tell your auth server to redirect to `https://oauth.click/foo/bar/baz` and you'll get redirected to `foo://bar/baz`

## Is this secure?

Technically? Sure. It uses a standard SSL certificate on a host with modern TLS protocols and settings. Redirect requests are not logged.

## Can I trust it?

If you use oauth.click for your app, you should be aware that a server you don't control will receive requests with authorization codes meant for your app. You should decide if you trust oauth.click not to do anything with that information.

## Why don't I just host my own https listener that redirects requests for me?

You should definitely use your own server if you are able. Only use oauth.click if you trust it more than you have the ability to build and maintain a secure server to receive your requests.

You might use oauth.click during development, and only set up a proper server for yourself when you're ready to go live. Up to you.

## Who would need this?

This was made for a developer writing an iOS app that consumes the Blizzard API.
https://us.battle.net/forums/en/bnet/topic/20753726613

## How do I set up my own https listener like this?

Just install nginx, set up some certs (I use Let's Encrypt), and take a look at nginx.conf here to see how it's done.
