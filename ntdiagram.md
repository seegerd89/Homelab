## Network Architecture
```mermaid

flowchart TB

%% ========== EXTERNAL ==========
subgraph External["External Layer"]
    Internet["Internet"]
    Cloudflare["Cloudflare DNS"]
end

%% ========== NETWORK ==========
subgraph Network["Internal Network"]
    Router["Router / Gateway"]
    PiHole["Pi-hole (DNS Filtering)"]
end

%% ========== INFRA ==========
subgraph Infrastructure["Core Infrastructure"]
    TrueNAS["TrueNAS Server"]
    Containers["Container Services\n(Jellyfin, Navidrome, Minecraft)"]
    KVM["Raspberry Pi 4\n(KVM over IP)"]
end

%% ========== CLIENTS ==========
subgraph Clients["Client Devices"]
    Devices["PC / Laptop / Smartphone"]
end

%% ========== ACCESS ==========
subgraph Access["Secure Access Layer"]
    Tailscale["Tailscale VPN (WireGuard)"]
end

%% ========== CONNECTIONS ==========

Internet --> Cloudflare --> Router

Router --> PiHole
Router --> TrueNAS
Router --> Devices

PiHole --> Devices

TrueNAS --> Containers
KVM --> TrueNAS

Devices --> Tailscale --> TrueNAS
```
