---
title: "AdSphere: Devlog"
description: "Bitirme Projesi: Markaları ve influencerları kampanyalar, içerik onayı, gönderi veya satış bazlı işlemler üzerinden ölçeklenebilir şekilde buluşturan bir platform."
status: active
started: 2025-09-08
---

# 🚧 Proje Durumu: Aktif

> **Başlangıç:** 8 Eylül 2025  
> **Hedef:** Derin İş Analizi & Haftalık Deployment & Mezuniyet  
> **Rol:** Takım Lideri & Sistem Mimarı & Full-Stack Geliştirici

---

### AdSphere Nedir?

AdSphere, bizim **Bitirme Projemiz** (Senior Design Project). Kendisi markalar ve influencerlar arasındaki boşluğu büyük ölçekte doldurmak için tasarlanmış, uçtan uca (full-stack) bir platform. Temel amaç; kampanya yönetimi ve içerik onayı gibi karmaşık iş akışlarını yönetirken, gönderi başı (post-based) veya komisyon bazlı (sale-based) işlemlerin ölçeklenebilir şekilde gerçekleşmesini sağlamaktır.

Bu seriyi yazmaktaki acmacım, ilk mimari kararlardan final deployment aşamasına kadar tüm mühendislik sürecini belgelemeyi amaçlasa da sürecin başlangıcından tam 3 ay sonra yazılmaya başladığımı not düşmek gerekir.

### Teknolojiler

Bu projeyi conteinerization ve temiz mimari (clean architecture) prensiplerine odaklanarak inşa ediyoruz.

| Bileşen | Teknoloji |
| :--- | :--- |
| **Frontend** | ReactJS (TypeScript) |
| **Backend** | Flask (Python) |
| **Veritabanı** | PostgreSQL |
| **DevOps** | Docker & Docker Compose |
| **Cloud** | GCP (E2 Instance) |

### 🚀 Bismillah

```shell
$ docker compose -f docker-compose.dev.yaml up --build

[+] Building 4.2s (17/17) FINISHED
 => [internal] load build definition from Dockerfile                     0.0s
 => [backend 6/6] RUN pip install -r requirements.txt                    1.5s
 => [frontend 6/6] RUN npm run build                                     2.4s
 => [db] pulled                                                          0.0s
[+] Running 4/4
 ✔ Network adsphere_net           Created                                0.1s
 ✔ Container adsphere-db-1        Started                                0.1s
 ✔ Container adsphere-backend-1   Started                                0.2s
 ✔ Container adsphere-frontend-1  Started                                0.2s
Attaching to adsphere-backend-1, adsphere-frontend-1...