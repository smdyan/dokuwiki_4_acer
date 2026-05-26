# acer_srv
Host is running services accessible through swag or localy via wg network

## Dokuwiki

* clone git repo
* build and run dokuwiki container 
    ```
        docker compose up -d
    ```
* container file location on host '/vlm_docker/dokuwiki/config/'
* update 'default.conf' at '/vlm_docker/dokuwiki/config/nginx/site-confs'. Change note: removed access on port:443. For update run 'bash ./conf_upd.sh';
* complete the setup by appending install.php to URL
* add dokuwiki pages to remote location 'dokuwiki/data/pages'


### Backup & restore Dokuwiki pages

* Create an archive and check files added
    ```bash
        tar -cf wiki_pages_25_12_18.tar  -C /vlm_docker/dokuwiki/config/dokuwiki/data/pages .
        tar -tf wiki_pages_date.tar'
    ```
* Copy from remote to local 
    ```bash
        scp user@host.ru:/home/user/vps/wiki_pages_date.tar ./
    ```

* Copy from local to remote 
    ```bash
        scp ./wiki_pages_date.tar acer:/home/smdyan/acer_srv
    ```
* Extract files to container volume 
    ```bash
        tar -xvf wiki_pages_date.tar -C /vlm_docker/dokuwiki/config/dokuwiki/data/pages
    ```
* Change UID and GID 
    ```bash
        sudo chown -R 1001:1001 ./pages/            # newuser:newgroup
    ```