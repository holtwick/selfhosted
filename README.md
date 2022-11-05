# selfhosted

> My personal choice of self-hosted apps. 

This project is accompanied by toots on Mastodon: [mastodon.social/@holtwick](https://mastodon.social/@holtwick).

## My Recommended Services

- [Gitea](gitea/docker-compose.yml) is a bit like Github, but for smaller groups. It helps you to manage code and tickets. But also provides a super easy registry for your private packages. it is tiny and fast. [-> gitea.io](https://gitea.io/)
- [Nextcloud](nextcloud/docker-compose.yml) is your "Cloud Service". I use it for file sharing mainly. But it can do most things Google and Apple offer as well, like mail, contacts, calendar, office tools. [-> nextcloud.com](https://nextcloud.com/)
- [LanguageTool](languagetool/docker-compose.yml) LanguageTool is your private instance of the best grammar and spell checker available. When you use this private instance, you have less to worry about non-public texts going through a public checking service. [-> languagetool.org](https://languagetool.org)

*More to come on a day by day basis...*

## Get Started

I run my stuff on a [cloud server instance at Hetzner](https://hetzner.cloud/?ref=thK9VpOJK5Sg). There I choose the "Docker" presets. Any other provider will probably work as well.

Then the first thing to do is to set up a [Nginx Proxy Manager](https://github.com/NginxProxyManager/nginx-proxy-manager). This is as easy as creating a folder named `proxy` and put this [`docker-compose.yml`](proxy/docker-compose.yml) file in it. Then start with `docker compose up -d`.

The proxy does two things:

1. It manages your projects
2. It manages your SSL certificates via Let's Encrypt

Now we can get started setting up more services. The best thing to do upfront is to configure a wildcard in your DNS, like `*.selfhosted.example.com` pointing to your cloud server instance.

## Setup Project

To install a project:

1. Copy the `docker-compose.yml` to a subfolder on your cloud server. 
2. Start it from there with `docker compose up -d`.
3. In the web interface of the Nginx Proxy create a "Proxy Host" with:
   - Domain Names: Something like `my.selfhosted.example.com`
   - Scheme: `http`
   - Forward Hostname / IP: The `container_name` you chose in the `docker-compose.yml`.
   - Forward Port: The port the service usually uses.
4. You can then also request the SSL certificate from there.

Please note, that each `docker-compose.yml` includes these lines:

```yml
networks:
  default:
    external:
      name: proxy
```

This is required to allow connection to the Nginx Proxy.

Another convention is to not use Docker volumes but redirect to a local `data` folder. This helps with backups and porting to other instances.
