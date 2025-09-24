---
title: Networks
description: 
published: true
date: 2025-09-24T18:40:36.645Z
tags: 
editor: markdown
dateCreated: 2025-09-24T18:22:42.282Z
---

```plantuml
@startuml
!theme spacelab

skinparam rectangle {
    BorderColor #A9A9A9
    FontColor white
}
skinparam package {
    BorderColor #666666
}
skinparam cloud {
    BorderColor #304d6d
}
skinparam arrow {
    FontColor black
}
skinparam note {
    FontColor black
}

' Define actors and boundaries
actor "User / Internet" as User
cloud "LAN (192.168.10.0/24)" as LAN

rectangle "Docker Host" as Host {

    ' --- HOST NETWORK ---
    ' Containers with direct access to the host's network interface
    package "Host Network" <<Node>> #LightSeaGreen {
        rectangle "adguardhome" as adguard #2F4F4F
        rectangle "plex" as plex #4B0082
        rectangle "glances" as glances #555555
    }

    ' --- FRONTEND NETWORK (DMZ) ---
    ' This is the primary entry point, managed by the reverse proxy
    package "frontend_net (DMZ)" <<Network>> #Orange {
        rectangle "npm" as npm #00008B
        note right of npm: Main entry point for all web traffic (Ports 80, 443)

        ' User-facing applications
        rectangle "organizr_new" as organizr #4B0082
        rectangle "overseerr" as overseerr #4B0082
        rectangle "immich-server" as immich_server #4B0082
        rectangle "paperless_new" as paperless #006400
        rectangle "mealie_new" as mealie #2F4F4F
        rectangle "wikijs" as wikijs #2F4F4F
        rectangle "ollama" as ollama #2F4F4F
        rectangle "filebrowser_new" as filebrowser #2F4F4F
        rectangle "code_server_new" as code_server #2F4F4F
        rectangle "firefox_new" as firefox #2F4F4F
        rectangle "authentik-server" as authentik_server #8B0000
        rectangle "whatsupdocker" as wud #555555
        rectangle "portnote" as portnote #2F4F4F
        rectangle "audiobookshelf" as audiobookshelf #4B0082
        rectangle "calibre" as calibre #4B0082
        rectangle "booklore" as booklore #4B0082
        rectangle "romm" as romm #4B0082
    }

    ' --- BACKEND NETWORK (Application Logic) ---
    ' Internal services that should not be directly exposed
    package "backend_net (Application)" <<Network>> #DodgerBlue {
        rectangle "sabnzbd" as sabnzbd #006400
        rectangle "radarr_hd / radarr_k" as radarr #006400
        rectangle "sonarr_hd / sonarr_k" as sonarr #006400
        rectangle "prowlarr" as prowlarr #006400
        rectangle "bazarr" as bazarr #006400
        rectangle "immich_machine_learning" as immich_ml #4B0082
        rectangle "authentik-worker" as authentik_worker #8B0000
        rectangle "readarr-audio" as readarr_audio #006400
        rectangle "readarr-ebook" as readarr_ebook #006400
    }

    ' --- DATABASE NETWORK (Data Layer) ---
    ' The most protected network, containing databases
    package "db_net (Data)" <<Network>> #Tomato {
        rectangle "Postgres" as postgres #8B4513
        rectangle "Redis" as redis #8B4513
        rectangle "MariaDB" as mariadb #8B4513
        rectangle "immich_postgres" as immich_pg #8B4513
        rectangle "immich_redis" as immich_redis #8B4513
    }

    ' --- MONITORING NETWORK ---
    ' Services dedicated to monitoring the health of the stack
    package "monitoring_net (Monitoring)" <<Network>> #Grey {
        rectangle "grafana_port" as grafana #555555
        rectangle "loki_port" as loki #555555
        rectangle "alloy" as alloy #555555
        rectangle "telegraf" as telegraf #555555
        rectangle "influxdb_port" as influxdb #555555
        rectangle "uptime-kuma_port" as uptime_kuma #555555
        rectangle "tautulli_port" as tautulli #555555
        rectangle "scrutiny" as scrutiny #555555
        rectangle "netdata_port" as netdata #555555
    }
}

' Define Relationships and Data Flow

' External Access
User --> npm : "HTTPS/80, 443"
LAN --> adguard : "DNS/53"
LAN --> plex : "32400"
LAN --> glances
LAN ..> npm : (Local DNS)

' Reverse Proxy Flow (Primary Path)
npm ..> organizr : "proxies to"
npm ..> paperless
npm ..> mealie
npm ..> authentik_server
npm ..> immich_server

' Frontend -> Backend Communication
immich_server --> immich_ml
authentik_server --> authentik_worker
radarr --> sabnzbd
sonarr --> sabnzbd

' Application -> Database Communication
paperless --> postgres
paperless --> redis
mealie --> postgres
wikijs --> postgres
authentik_server --> postgres
authentik_worker --> postgres
portnote --> postgres
booklore --> mariadb
romm --> mariadb

' Immich's self-contained backend
immich_server --> immich_pg
immich_server --> immich_redis

' Monitoring Connections
tautulli ..> plex : "Monitors Plex API"
telegraf ..> influxdb : "Writes Metrics"
grafana ..> influxdb : "Reads Metrics"
telegraf ..> radarr : "Scrapes /metrics"
telegraf ..> sonarr : "Scrapes /metrics"
alloy ..> loki : "Forwards Logs"
netdata ..> Host : "Monitors Host"

' Layout helpers
sabnzbd -[hidden]right- radarr
prowlarr -[hidden]right- sonarr

@enduml


```