# MQTT
Containers
- [Mosquitto](https://mosquitto.org) - MQTT-server
- [MQTT-Explorer](https://mqtt-explorer.com) - MQTT-client


# Mosquitto
https://mosquitto.org

start/restart/stop container
```sh
docker-compose up -d
docker-compose restart
docker-compose down
```


## Users / Passwords
users/passwords are stored in [/mosquitto/config/mosquitto.passwd](./conf/mosquitto.passwd) file, which is specified as `password_file` in [/mosquitto/config/mosquitto.conf](./conf/mosquitto.conf)
```
password_file /mosquitto/config/mosquitto.passwd
```

Adding users to passwd-file
```sh
# logon into mqtt-container
docker exec -it  -u 1883 mosquitto-mosquitto-1 sh

# navigate to passwd-file
cd /mosquitto/config/
cat mosquitto.passwd
mosquitto_passwd -c mosquitto.passwd user_name  # clear/create passwd-file, add user/password
mosquitto_passwd mosquitto.passwd user_name     # add user/password
mosquitto_passwd -D mosquitto.passwd user_name  # delete user/password
mosquitto_passwd -U mosquitto.passwd            # convert passwords from plaintext to hashed
chmod u+rw,g+rw,o-rw mosquitto.passwd           # update access rights
```

! restart mqtt-server after changing password-file
```sh
docker compose restart
```


## Log
Check log-file [log/mosquitto.log](./log/mosquitto.log)


# MQTT-Explorer
https://mqtt-explorer.com
- github: https://github.com/thomasnordquist/MQTT-Explorer

```sh
docker compose build mqttexplorer

docker-compose up -d
docker-compose down
docker logs mosquitto_mosquitto_1 --follow
```


# References
- https://cedalo.com/blog/mosquitto-docker-configuration-ultimate-guide/
- https://www.laub-home.de/wiki/Eclipse_Mosquitto_Secure_MQTT_Broker_Docker_Installation
- https://github.com/thomasnordquist/MQTT-Explorer