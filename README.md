# Heroku buildpack for autossh
This is a Heroku buildpack that adds `autossh` to your heroku build and starts it, pointing at a given tunnel and target host and port.

(`autossh` is a program to start a copy of ssh and monitor it, restarting
it as necessary should it die or stop passing traffic. More information about autossh can be found here: <http://www.harding.motd.ca/autossh/>)

## Usage

```
$ heroku create --buildpack https://github.com/heroku/heroku-buildpack-multi.git
```

In your project add a `.buildpacks` file.

```
# .buildpacks
https://github.com/Adcolony-Engineering/heroku-buildpack-autossh.git
https://github.com/heroku/heroku-buildpack-ruby.git#v138
```

Then set the following environment variables in your Heroku app:

- `SSH_TUNNEL_PUBLIC_KEY`: the public SSH key for the tunnel
- `SSH_TUNNEL_PRIVATE_KEY`: the public SSH key for the tunnel
- `SSH_TUNNEL_IP`: the IP of the SSH tunnel machine to use
- `SSH_TUNNEL_TARGET_HOST`: the host to tunnel to
- `SSH_TUNNEL_TARGET_PORT`: the port to tunnel to

Additionally, you can optionally set the following:

- `SSH_TUNNEL_LISTEN_PORT`: the local port to forward traffic to the target over
      (default: 29177)

Then, instead of connecting to 

```
http://$SSH_TUNNEL_TARGET_HOST:$SSH_TUNNEL_TARGET_PORT
```

you can connect to 

```
http:://localhost:$SSH_TUNNEL_LISTEN_PORT
```

## Questions? 
Ask @josh.conner or @azi.

