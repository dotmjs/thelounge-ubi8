# thelounge-ubi8 #

The Lounge is a web based IRC client
This file is a Dockerfile, to provide an instance of The Lounge running on your desktop, under your account, easily built and run non-root, using podman, and managed by systemd's user service

--------------------

## Build the container (non-root) ##
```
podman build -t thelounge  . -f thelounge.Dockerfile 
```

## Run a single instance under podman ##
```
mkdir -p ~/.thelounge
podman run -d --rm --publish 127.0.0.1:9000:9000 --volume ~/.thelounge:/var/opt/thelounge:Z --env USER --name thelounge thelounge
```

## Optional: Create systemd user unit files (non-root) ##
```
mkdir -p ~/.config/systemd/user
podman generate systemd --new  thelounge > ~/.config/systemd/user/thelounge.service
podman kill thelounge
```

## Optional: Run the following to start thelounge on login (and now) (non-root) ##
```
systemctl --user enable --now  thelounge
systemctl --user status thelounge
```

## Connect to thelounge ##
- Open Web Browser to http://localhost:9000
- login with username same as your desktop login, password is "password"
