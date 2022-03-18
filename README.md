<p align="center">
    <img src="https://media.discordapp.net/attachments/938248997733273602/954490232609312808/small-waves-icon-cartoon-style-vector-11250045-removebg-preview.png?width=381&height=411"
        height="300">
</p>
<p align="center">
    <a href="https://discord.gg/thingsunblocks">
        <img src="https://img.shields.io/discord/419123358698045453?style=for-the-badge&logo=discord"
            alt="chat on Discord"></a>
</p>
<p align="center">
Surf The Web With Invaldia At Anytime!

## Hosting Services
<a href="https://heroku.com/deploy?template=https://github.com/Degenerate0001/Degeneracy"><img height="30px" src="https://raw.githubusercontent.com/FogNetwork/Tsunami/main/deploy/heroku2.svg"><img></a>
<a href="https://repl.it/github/EngineXNetwork/Invaldia"><img height="30px" src="https://raw.githubusercontent.com/FogNetwork/Tsunami/main/deploy/replit2.svg"><img></a>

# Table Of Contents
- [Installation and Setup](#Installation-and-Setup)
- [Configuration](#Configuration)
  - [Default Config](#Default-Config-Example)
  - [Persistance](#Persistance-With-PM2)
- [Nginx Config](#Nginx)
  - [Letsencrypt](#Letsencrypt)
   - [Cron](#Cron)
- [FAQ](#Frequently-Asked-Questions)
- [Support](#Support)
- [Proxy Sources](#Proxy-Sources)
- [License](#License)
- [Donations](#Donations)

# Installation and Setup

```sh
$ git clone https://github.com/EngineXNetwork/Invaldia
$ cd Invaldia
$ npm install
$ chmod u+x main.sh
$ ./main.sh
```

# Configuration

Configure Invaldia in `config.json`.

## Default Config Example:

```js
self.__uv$config = {
    prefix: '/service/',
    bare: '/bare/',
    encodeUrl: Ultraviolet.codec.xor.encode,
    decodeUrl: Ultraviolet.codec.xor.decode,
    handler: '/uv/uv.handler.js',
    bundle: '/uv/uv.bundle.js',
    config: '/uv/uv.config.js',
    sw: '/uv/uv.sw.js',
};
```
* Prefix: The prefix you want for Corrosion. (recomended that you keep it the same)
* Codec: Basic encryption method for filter evasion in Corrosion. (Options include `xor`, `base64`, or `plain`. xor or base64 are recommended)

# Persistance With PM2

I have listed PM2 as a method for persistance as it is easy to work with, and it offers server monitoring.

To get started, run the following commands:

```sh
$ npm i pm2 -g
$ pm2 start start.js
$ pm2 startup
$ pm2 save
```
Run the first command outside of the `Invaldia` directory.

# Nginx
Set up Nginx to serve Degeneracy and obtain Letsencrypt certificates using Certbot.

Run the following commands to install Nginx and Certbot (skip this step if you already have both installed):

```
$ apt install -y nginx python3 python3-venv libaugeas0
$ python3 -m venv /opt/certbot/
$ /opt/certbot/bin/pip install --upgrade pip
$ /opt/certbot/bin/pip install certbot certbot-nginx
$ ln -s /opt/certbot/bin/certbot /usr/bin/certbot
```

Note: each line above is a separate command.

Next, create the following file in `/etc/nginx/sites-enabled/degeneracy`.

```nginx
server {
    server_name your.domain.com; # Replace with your actual domain
    location / {
        proxy_set_header Accept-Encoding "";
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-Host $host:$server_port;
        proxy_set_header X-Forwarded-Server $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";   
        proxy_pass https://127.0.0.1:8443;  # change to http if ssl is set to false
        proxy_http_version 1.1; 
        proxy_set_header Host $host;
    }
    # Uncomment the block below this to block GoogleBot
    #location / { 
    #   if ($http_user_agent ~ (Googlebot) ) {
    #       return 403;
    #}
    
    listen 80;
}
```

## Letsencrypt

Run these commands to get certificates for your site. Certbot will make this easy!

```
$ certbot --nginx -d <insert your domain here>
$ systemctl restart nginx
```

### Cron

If you would like, you can setup a cron job to automatically renew your certificates once they expire. To do this, run the following command.

```
$ crontab -e
```

Here you may be prompted to choose a text editor. The default will be just fine for our purposes. After you are brought into the file, add the following line to it.

```
0 12 * * * /usr/bin/certbot renew --quiet
```

This will check every day at noon if your certs are about to expire. If they are, they will be silently renewed. By doing this, you'll never really have to worry about certs again after your initial install and setup.

# Frequently Asked Questions

A compilation of some frequently asked questions, and short answers for them.
    
| Question | Answer |
| -------- | ------ |
| Why do I keep getting 404 errors? | The most likely reason is that you are entering a path that doesn't exist. Ex: invaldia.enginexnetwork.repl.co/foo. If you know this isn't the case and it is something else, please open an issue. |
| Why is a site marked as deceptive? | Google will sometimes mistake a proxy site for a scam/phishing site. The best thing you can do in this situation is to report it as a mistake [here](https://safebrowsing.google.com/safebrowsing/report_error/?hl=en). |
| Where can I get more links? | You can get more links by clicking the "Community" button on the homepage, or by going to [discord.gg/thingsunblocks](https://discord.gg/thingsunblocks). There I will have more links posted, and you can check out other cool proxy sites! |
| Why is it when I click on a button, nothing happens? | Sometimes caching leads to a button not working. Try pressing `crtl + shift + r` to fix this. If the issue persists, open an issue. |
| What if my issue isn't listed on here? | No worries! You can contact me by email (floppa@enginexnetwork.gq), Discord (floppaaa#0001), or by opening an issue. |

# Support

For any questions, comments, or concerns, please open an issue, contact me on Discord: `@floppaaa#0001`,or contact me by email: `floppa@enginexnetwork.gq`.

# Proxy Sources
    
[Ultraviolet](https://github.com/titaniumnetwork-dev/ultraviolet)
    
[Corrosion](https://github.com/titaniumnetwork-dev/Corrosion) (Mostly deprecated thanks to Ultraviolet)
    
[Womginx](https://github.com/binary-person/Womginx)
    
[Rammerhead](https://rammerhead.org) (Not open-source so I linked to the official site)

# Donations

If you would like to contribute to the project via donation, send in some crypto or subscribe to the [Patreon](https://patreon.com/japondeeznuts)! Your donation/contribution is very much appreciated :D