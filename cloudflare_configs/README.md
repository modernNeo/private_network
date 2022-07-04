
[Cloudflare Zero Trust](https://dash.teams.cloudflare.com) 

# Setup Public Hostname

![Screenshot](.screenshots/public_hostname_config.png)

`nginx:80` -> `<key associated with nginx docker app in the docker-compose.yml>:<port listed in nginx_configs/steelbooks>`

# Generate .Env file

 1. go to https://dash.teams.cloudflare.com
 2. `Access` -> `Tunnels` -> Click on `Configure` for tunnel 
 3. get the token from the command `sudo cloudflared service install <TOKEN>` on the website
 4. Place token in `cloudflare.env`

# Generate Credentials file

Run from inside docker container ubuntu
```shell
docker exec -it ubuntu_container bash
apt-get update
curl -L --output cloudflared.deb https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb && sudo dpkg -i cloudflared.deb && 

cloudflared service install ${TOKEN}
cloudflared tunnel login
cloudflared tunnel list
cloudflared tunnel token --cred-file credentials.json <Tunnel UUID>
exit
docker cp ecstatic_northcutt:/credentials.json /var/services/homes/jace/private_network/cloudflare_configs/credentials.json
```