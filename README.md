# ghost-automatic-backup
Simplest scheme to automatically backup your ghost blog.

# Step 1: Setup Ghost Backup

This will launch whitelisting based selective sync as container.

```
docker-compose -f docker-compose-dropbox.yml up -d
```

To register host with Dropbox follow the link provided in the logs.

```
docker logs -f ghost-backup-automatically_dropbox_1
```

Make sure data sync is complete before launch ghost blog in the next up. This is essential because all the data needs to be written to the docker volume created in the first step before this volume is attached to the ghost blog.

```
docker exec -it ghost-backup-automatically_dropbox_1 dropbox status
docker exec -it ghost-backup-automatically_dropbox_1 dropbox exclude
docker exec -it ghost-backup-automatically_dropbox_1 find ghost
```

# Step 2: Launch Blog

This will launch your ghost blog as a docker container.

```
docker-compose -f docker-compose-myblog.yml up -d
```
