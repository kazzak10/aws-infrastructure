# AWS Cloud Infrastructure Setup

![AWS](https://img.shields.io/badge/AWS-Cloud-FF9900?logo=amazonaws&logoColor=white)
![EC2](https://img.shields.io/badge/EC2-Compute-FF9900?logo=amazonaws&logoColor=white)
![S3](https://img.shields.io/badge/S3-Storage-FF9900?logo=amazonaws&logoColor=white)
![RDS](https://img.shields.io/badge/RDS-Database-FF9900?logo=amazonaws&logoColor=white)

---

## 1. Executive Summary

Déploiement d'une infrastructure cloud complète sur AWS dans le cadre d'un projet de formation à l'ESGI Paris. L'objectif : configurer de A à Z les services fondamentaux d'une startup — réseau isolé, gestion des accès, stockage, base de données et serveur de calcul — en suivant les bonnes pratiques cloud et en restant dans le cadre Free Tier.

---

## 2. Business Problem

Une jeune startup a besoin d'une infrastructure cloud fiable, sécurisée et scalable pour héberger son application. Les contraintes sont réelles : budget limité (Free Tier), sécurité des accès, isolation du réseau et haute disponibilité des données.

---

## 3. Methodology

### Architecture déployée

```
Internet
    │
    └── Internet Gateway (esgi-igw)
            │
        VPC (10.0.0.0/16)
            │
        Subnet Public (10.0.1.0/24)
            │
    ┌───────┴────────┐
   EC2            RDS (esgi-db)
 (t2.micro)      MySQL · Free Tier
    │
Security Group
(SSH + HTTP)
```

### Services configurés

**Partie 1 — Réseau (VPC)**

- VPC `esgi-vpc` avec bloc CIDR `10.0.0.0/16`
- Sous-réseau public `esgi-subnet-public` : `10.0.1.0/24`
- Internet Gateway `esgi-igw` attachée au VPC
- Table de routage configurée pour diriger le trafic sortant vers l'IGW

**Partie 2 — Sécurité (IAM)**

- Groupe `Developpeurs` avec politique `EsgiAppPolicy`
- Policy IAM autorisant lecture S3 (`s3:GetObject`, `s3:ListBucket`)
- Utilisateur `dev-user` créé et ajouté au groupe

**Partie 3 — Stockage (S3)**

- Bucket `esgi-assets-houari-zakaria` créé
- Fichier `hello-esgi.txt` uploadé
- Accès public bloqué par défaut

**Partie 4 — Base de données (RDS)**

- Instance `esgi-db` MySQL Community
- Modèle Free Tier — stockage 20 Go
- Statut : Disponible

**Partie 5 — Calcul (EC2)**

- Instance `t2.micro` Amazon Linux dans `esgi-subnet-public`
- IP publique : `15.237.117.128`
- Security Group `esgi-web-sg` : SSH (port 22) + HTTP (port 80)
- Connexion SSH établie depuis terminal

---

## 4. Skills

| Service | Usage                                                 |
| ------- | ----------------------------------------------------- |
| **VPC** | Réseau isolé, sous-réseaux, routing, Internet Gateway |
| **IAM** | Groupes, policies, utilisateurs, gestion des droits   |
| **S3**  | Bucket, upload d'objets, gestion des accès            |
| **RDS** | Instance MySQL, configuration Free Tier               |
| **EC2** | Instance Linux, security groups, connexion SSH        |

---

## 5. Screenshots

### VPC — Réseau

![VPC](screenshots/01_vpc.png)

### IAM — Gestion des accès

![IAM](screenshots/02_iam.png)

### S3 — Stockage

![S3](screenshots/03_s3.png)

### RDS — Base de données

![RDS](screenshots/04_rds.png)

### EC2 — Calcul

![EC2](screenshots/05_ec2.png)

---

## 6. Results & Key Takeaways

Infrastructure cloud complète déployée en autonomie sur AWS Free Tier, sans frais supplémentaires.

**Ce que ce projet m'a appris :**

- Comprendre l'isolation réseau avec VPC et la gestion du routage
- Appliquer le principe du moindre privilège avec IAM
- Différencier les services de stockage (S3 objet vs RDS relationnel)
- Connecter et sécuriser une instance EC2 avec SSH et security groups

---

## Auteur

**Zakaria Houari** · Étudiant Bachelor Informatique spécialité IA/Data · ESGI Paris

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Zakaria_Houari-0077B5?logo=linkedin)](www.linkedin.com/in/zakaria-houari-775259351)
[![GitHub](https://img.shields.io/badge/GitHub-@kazzak10-181717?logo=github)](https://github.com/kazzak10)
[![Portfolio](https://img.shields.io/badge/Portfolio-portfoliohouari.netlify.app-orange)](https://zakariahouari.netlify.app)
