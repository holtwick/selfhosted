# selfhosted

My personal choice of self hosted apps. 

I run my stuff on a [cloud server instance at Hetzner](https://hetzner.cloud/?ref=thK9VpOJK5Sg). There I choose the "Docker" presets. Any other provider will probably work as well.

Then the first thing to do is to set up a [Nginx Proxy Manager](https://github.com/NginxProxyManager/nginx-proxy-manager). This is as easy as creating a folder named `proxy` and put this `docker-compose.yml` file in it. Then start with `docker compose up -d`.

The proxy does two things:

1. It manages your projects
2. It manages your SSL certificates via Let's Encrypt

Now we can get started setting up more services. The best thing to do upfront is to configure a wildcard in your DNS, like `*.selfhosted.example.com` pointing to your cloud server instance.
