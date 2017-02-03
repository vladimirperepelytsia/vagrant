#Vagrant for php projects

* install or update to latest version virtualbox
* install or update to latest version vagrant
* install ansible
* install vagrant hosmanager
* copy config.default.yml and rename as config.yml
    * set network settings
    * set id_rsa_path for your local id_rsa key
    * set mysql credentials in config.yml
    * add project data to projects in config.yml
        Project data example
        name: "web.local",
        local_path: "/projects/web.local",
        virtual_path: "/var/www/web.local",
        webroot: "/var/www/web.local",
        database: "db_name",
        git_repo: ""  (or hg repo)
