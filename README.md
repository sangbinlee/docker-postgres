# docker-postgres
docker-postgresql



 
# sudo usermod -aG docker $USER
                
        현재 계정을 docker 2차그룹에 추가 ?



        
        사용자한테 그룹 추가하기
        usermod -a -G [group] [사용자아이디]
        
        
        
        
        
        사용자 그룹을 변경하기
        
        usermod -g [group] [사용자아이디]
        
        이렇게하면 사용자의 그룹이 [group]으로 변경됨. 나머지 것들은 다 삭제됨
        
        
        해당 폴더의 그룹 소유권을 변경
        chown [소유자]:[그룹] [폴더이름]
        
              
        해당 폴더의 소유자와 그룹을 변경한다. 
        
        
        해당 폴더의 권한 변경
        chmod xxx [폴더이름]
        
                
        이 때 xxx에는 0~7사이의 숫자가 들어갑니다. 
        이 숫자에 따라서 소유자권한, 그룹권한, 기타 사용자권한이 나뉜다. 
        

# 현재 사용자 
         
        sangbinlee9@master:~$ echo $USER
        sangbinlee9
        sangbinlee9@master:~$


# 그룹 목록 
        Last login: Sun Oct  8 09:23:20 2023 from 192.168.0.108
        sangbinlee9@master:~$
        sangbinlee9@master:~$ cat /etc/group
        root:x:0:
        daemon:x:1:
        bin:x:2:
        sys:x:3:
        adm:x:4:syslog,sangbinlee9
        tty:x:5:
        disk:x:6:
        lp:x:7:
        mail:x:8:
        news:x:9:
        uucp:x:10:
        man:x:12:
        proxy:x:13:
        kmem:x:15:
        dialout:x:20:
        fax:x:21:
        voice:x:22:
        cdrom:x:24:sangbinlee9
        floppy:x:25:
        tape:x:26:
        sudo:x:27:sangbinlee9
        audio:x:29:
        dip:x:30:sangbinlee9
        www-data:x:33:
        backup:x:34:
        operator:x:37:
        list:x:38:
        irc:x:39:
        src:x:40:
        gnats:x:41:
        shadow:x:42:
        utmp:x:43:
        video:x:44:
        sasl:x:45:
        plugdev:x:46:sangbinlee9
        staff:x:50:
        games:x:60:
        users:x:100:
        nogroup:x:65534:
        systemd-journal:x:101:
        systemd-network:x:102:
        systemd-resolve:x:103:
        messagebus:x:104:
        systemd-timesync:x:105:
        input:x:106:
        sgx:x:107:
        kvm:x:108:
        render:x:109:
        lxd:x:110:sangbinlee9
        _ssh:x:111:
        crontab:x:112:
        syslog:x:113:
        uuidd:x:114:
        tcpdump:x:115:
        tss:x:116:
        landscape:x:117:
        fwupd-refresh:x:118:
        netdev:x:119:
        sangbinlee9:x:1000:
        docker:x:999:
        sangbinlee9@master:~$







# 
    mkdir -p /data/postgresql/data
    mkdir -p /data/postgresql/pgadmin


# docker-compose.yml

    version: '3.6'
    
    services:
      postgres:
        container_name: postgres
        image: postgres:10
        restart: unless-stopped
        environment:
          - POSTGRES_PASSWORD='비밀번호'
          - TZ=Asia/Seoul
        volumes:
          - /data/postgresql/data:/var/lib/postgresql/data
        ports:
          - "5432:5432"
    
      pgadmin:
        container_name: pgadmin
        image: dpage/pgadmin4
        restart: unless-stopped
        ports:
          - "5555:80"
        volumes:
          - /data/postgresql/pgadmin:/var/lib/pgadmin
        environment:
          - PGADMIN_DEFAULT_EMAIL=ducj@pgadmin.com
          - PGADMIN_DEFAULT_PASSWORD=비밀번호
          - TZ=Asia/Seoul
        depends_on:
          - postgres





#

        
        
        version: '3.6'
        
        services:
          postgres:
            container_name: postgres
            image: postgres:10
            environment:
              - POSTGRES_PASSWORD=XXXX
              - TZ=Asia/Seoul
            volumes:
              - /mnt/postgres/data:/var/lib/postgresql/data
            ports:
              - "5432:5432"
        
          pgadmin:
            container_name: pgadmin
            image: dpage/pgadmin4
            restart: on-failure
            ports:
              - "5555:80"
            volumes:
              - /mnt/pgadmin/data:/var/lib/pgadmin
            environment:
              - PGADMIN_DEFAULT_EMAIL=XXX@pgadmin.com
              - PGADMIN_DEFAULT_PASSWORD=XXXX
              - TZ=Asia/Seoul
            depends_on:
              - postgres
