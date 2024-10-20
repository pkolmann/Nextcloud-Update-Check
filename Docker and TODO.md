# Run Docker Container
```bash
docker run -d -p 8080:80 --name nextcloud28 nextcloud:28.0.1
```

## Finish install when occ is not available
```bash
docker exec -u www-data nextcloud28 php occ maintenance:install --admin-user "admin" --admin-pass "admin"
```

## Set Token for Nextcloud ServerInfo
```bash
docker exec -u www-data nextcloud28 php occ config:app:set serverinfo token --value "1234567890"
```

## Access ServerInfo
```bash
curl -4H "NC-Token: 1234567890" "http://localhost:8080/ocs/v2.php/apps/serverinfo/api/v1/info?format=json&skipApps=false&skipUpdate=false" | jq .
```

# Events to listen to:

* App Update Event: https://docs.nextcloud.com/server/latest/developer_manual/basics/events.html#ocp-app-events-appupdateevent
* https://docs.nextcloud.com/server/latest/developer_manual/basics/events.html#ocp-app-managerevent