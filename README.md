# mvdmio notes

To merge upstream changes, run:

```
git pull --rebase upstream main

```

# Fizzy

This is the source code of [Fizzy](https://fizzy.do/), the Kanban tracking tool for issues and ideas by [37signals](https://37signals.com).

## Deploying Fizzy

If you'd like to run Fizzy on your own server, we recommend deploying it with [Kamal](https://kamal-deploy.org/).
Kamal makes it easier to set up a bare server, copy the application to it, and manage the configuration settings that it uses.

(Kamal is also what we use to deploy Fizzy at 37signals. If you're curious about what our deployment configuration looks like, you can find it inside [`fizzy-saas`](https://github.com/basecamp/fizzy-saas).)

This repo contains a starter deployment file that you can modify for your own specific use. That file lives at [config/deploy.yml](config/deploy.yml), which is the default place where Kamal will look for it.

The steps to configure your very own Fizzy are:

1. Fork the repo
2. Edit few things in config/deploy.yml and .kamal/secrets
3. Run `kamal setup` to do your first deploy.

We'll go through each of these in turn.

### Fork the repo

To make it easy to customise Fizzy's settings for your own instance, you should start by creating your own GitHub fork of the repo.
That allows you to commit your changes, and track them over time.
You can always re-sync your fork to pick up new changes from the main repo over time.

Once you've got your fork ready, run `bin/setup` from within it, to make sure everything is installed.

### Editing the configuration

The config/deploy.yml has been mostly set up for you, but you'll need to fill out some sections that are specific to your instance.
To get started, the parts you need to change are all in the "About your deployment" section.
We've added comments to that file to highlight what each setting needs to be, but the main ones are:

-  `servers/web`: Enter the hostname of the server you're deploying to here. This should be an address that you can access via `ssh`.
-  `ssh/user`: If you access your server a `root` you can leave this alone; if you use a different user, set it here.
-  `proxy/ssl` and `proxy/host`: Kamal can set up SSL certificates for you automatically. To enable that, set the hostname again as `host`. If you don't want SSL for some reason, you can set `ssl: false` to turn it off.
-  `env/clear/MAILER_FROM_ADDRESS`: This is the email address that Fizzy will send emails from. It should usually be an address from the same domain where you're running Fizzy.
-  `env/clear/SMTP_ADDRESS`: The address of an SMTP server that you can send email through. You can use a 3rd-party service for this, like Sendgrid or Postmark, in which case their documentation will tell you what to use for this.

Fizzy also requires a few environment variables to be set up, some of which contain secrets.
The simplest way to do this is to put them in a file called `.kamal/secrets`.
Because this file will contain secret credentials, it's important that you DON'T CHECK THIS FILE INTO YOUR REPO! You can add the filename to `.gitignore` to ensure you don't commit this file accidentally.

## Running your own Fizzy instance

If you want to run your own Fizzy instance, but don't need to change its code, you can use our pre-built Docker image.
You'll need access to a server on which you can run Docker, and you'll need to configure some options to customize your installation.

You can find the details of how to do a Docker-based deployment in our [Docker deployment guide](docs/docker-deployment.md).

If you want more flexibility to customize your Fizzy installation by changing its code, and deploy those changes to your server, then we recommend you deploy Fizzy with Kamal. You can find a complete walkthrough of doing that in our [Kamal deployment guide](docs/kamal-deployment.md).


## Development

You are welcome -- and encouraged -- to modify Fizzy to your liking.
Please see our [Development guide](docs/development.md) for how to get Fizzy set up for local development.


## Contributing

We welcome contributions! Please read our [style guide](STYLE.md) before submitting code.


## License

Fizzy is released under the [O'Saasy License](LICENSE.md).
