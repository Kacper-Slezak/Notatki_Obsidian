---
tags:
  - Cloud
  - XaaS
---


Chmura to nie tylko "cudzy komputer", to model **On-demand self-service**.

### Modele Usługowe (XaaS)

- **IaaS (Infrastruktura):** Dostajesz VM, sieć, storage. Ty zarządzasz OS (np. Amazon EC2, Linode).
    
- **PaaS (Platforma):** Skupiasz się na kodzie, chmura zarządza OS i runtime (np. Heroku).
    
- **SaaS (Oprogramowanie):** Gotowa aplikacja (np. Gmail, Office 365).
    
- **FaaS (Serverless):** Kod wyzwalany zdarzeniami (np. AWS Lambda).
    

### Modele Wdrożeniowe

- **Public:** Współdzielona infrastruktura (najtańsza, skalowalna).
    
- **Private:** Tylko dla jednej organizacji (bezpieczeństwo, compliance).
    
- **Hybrid:** Połączenie on-premises z chmurą publiczną.
    

### Automatyzacja (The Practical Side)

W nowoczesnej chmurze nie klikamy w panelu. Używamy:

- **API / CLI:** np. `curl -X POST api.linode.com/v4/linode/instances`.
    
- **Terraform / Ansible:** Zarządzanie infrastrukturą jako kod (**IaC**).