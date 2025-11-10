# ☸️ Projeto Kubernetes Deployments

> Este repositório contém os **manifests Kubernetes** utilizados para o deploy automatizado da aplicação **API** hospedada em outro repositório.

---

## 🔗 Origem da Aplicação

A aplicação **não está neste repositório** — ela é desenvolvida e versionada no repositório:

👉 [otaviolxna/projeto-uol-api](https://github.com/otaviolxna/projeto-uol-api)

A pipeline de **CI/CD** desse repositório é responsável por:
1. Construir e enviar a imagem Docker para o **Docker Hub** (`otaviolxna/hello-app`);
2. Atualizar automaticamente este repositório, alterando a **tag da imagem** no arquivo `deployment.yaml`;
3. O **Argo CD**, configurado no cluster Kubernetes, monitora este repositório e aplica as atualizações automaticamente.

---

## 🧩 Estrutura

```bash
.
├── deployment.yaml   # Define o Deployment da aplicação (imagem, réplicas, probes etc)
└── service.yaml      # Define o Service (porta 8080 → 8080)
```

---

## 📦 Container da Aplicação

As imagens são hospedadas publicamente em:  
📦 [Docker Hub - otaviolxna/hello-app](https://hub.docker.com/r/otaviolxna/hello-app)

---

## 🔁 Como funciona a automação

1. Quando há **commit** no repositório da API (`projeto-uol-api`), o GitHub Actions:
   - Constrói uma nova imagem Docker.
   - Atualiza o `deployment.yaml` neste repositório com a nova tag.
   - Faz **push** automaticamente (via SSH Deploy Key).
2. O **Argo CD** detecta a mudança e sincroniza o estado desejado com o cluster local.
3. O novo **Pod** é criado automaticamente com a nova versão.

---

## 👤 Autor

📌 **Otávio Lana**  
💻 Estudante de Segurança da Informação | DevSecOps & Cloud Security  
🌐 [LinkedIn](https://www.linkedin.com/in/otaviolxna) • [GitHub](https://github.com/otaviolxna)
