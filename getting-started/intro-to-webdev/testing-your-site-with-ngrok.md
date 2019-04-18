---
title: Testing Your Site With ngrok
layout: topic
categories: guide
---

# Testing Your Server with `ngrok`

[ngrok][ngrok] is a tool for testing your server
with a public-facing URL.
You can use it to test on mobile, share with your friends,
and set up webhooks.

It's a great tool for hackathons because of how quickly it
can be set up, since it doesn't require messing with DNS settings, port forwarding, firewalls, or deploying to another machine.

## When to use ngrok

`ngrok` works great in these scenarios:

- When you want to check your server on another device
- When you are setting up webhooks in your development environment
- When you are debugging your server in your development environment
- When you want to test your website on mobile
- or when you want to quickly share your work with others

## When not to use ngrok

However, `ngrok` is not a perfect solution for every use-case. Don't
use `ngrok` to:

- Host static content, like HTML that isn't going to change
- Replace your production server, as your URL will change with each use

It's OK for demos, but a dedicated server with a fixed IP may be more reliable.

# Getting Started

[`ngrok` already has some pretty good documentation, but I'll repeat
the steps here.](https://dashboard.ngrok.com/get-started)

## Download and Install the client

[Navigate to the Dashboard.](https://dashboard.ngrok.com/get-started)

Once you've created an account or logged in, the website will
provide a link where you can download the client.
It's available for Linux, Windows, and Mac.

As in the website's instructions, unzip the binary from the
archive you downloaded. They suggest placing the binary in a
user folder or aliasing it so that you can easily access it.

On Windows, a convienient path for you may be `C:\ngrok.exe`. On
Linux or Mac, under your home directory should be fine: `~/ngrok`.

## Authorize the Client

The dashboard page should provide a command that
you can run that will link your computer's ngrok client to your account.
Copy and paste this command into your command line to get connected.

**This token is sensitive information, so do not share it with others!**

## Start `ngrok`

[The `ngrok` docs are pretty good for this, but `ngrok help` works too.](https://ngrok.com/docs)

If you have a web server running on port 80, you can expose it using
`ngrok http 80`.

The application will then generate a random URL that will point to your
server. Try it out by opening it in your browser or on your phone.

Note that when restarting `ngrok`, your URL will randomly change.
Don't hard-code links that depend on your temporary URL, as things
will break!

### Debugging with `ngrok`

When the `ngrok` application is running, the console window will log
the connections that are established to your server.
It'll also include the link where you can access your site.

To expose an application running locally on port `8080` for HTTP
traffic, I can run the following command:

```console
$ ~/ngrok http 8080
```

![Screenshot of the ngrok console application](/uploads/ngrok2.png)

You can also view this same information by opening [localhost:4040](http://localhost:4040) in your browser.

![screenshot of the ngrok web debugger in use](/uploads/ngrok.png)

[ngrok]: https://ngrok.com/
