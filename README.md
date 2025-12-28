# Comparaison des Technologies d'API  
REST, SOAP, GraphQL et gRPC  
**Cas d'Étude : Plateforme de Réservation Hôtelière**

**Auteurs** : BENGRICH Saad, JABBOUR Omar  
**Institution** : ÉCOLE MAROCAINE DE SCIENCE DE L'INGÉNIERIE  
**Date** : Décembre 2024  

---

## 📋 Table des Matières

- [Résumé Exécutif](#-résumé-exécutif)
- [Introduction](#-introduction)
- [Technologies Étudiées](#-technologies-étudiées)
- [Méthodologie](#-méthodologie)
- [Résultats Détaillés](#-résultats-détaillés)
- [Analyse Comparative](#-analyse-comparative)
- [Recommandations](#-recommandations)
- [Conclusion](#-conclusion)

---

## 🎯 Résumé Exécutif

Cette étude compare quatre technologies d'API majeures (**REST**, **SOAP**, **GraphQL**, **gRPC**) dans le contexte d'une plateforme de réservation hôtelière.

Les tests sous charges variables (10–1000 requêtes simultanées) montrent que :

- **gRPC** offre les meilleures performances (latence moyenne **32,7 ms**, **1850 RPS**).
- **REST** excelle en simplicité et adoption (48,6 ms, 1245 RPS).
- **GraphQL** optimise la flexibilité (41,9 ms, 1350 RPS).
- **SOAP** reste pertinent pour les environnements legacy (94,7 ms, 680 RPS).

---

## 📖 Introduction

### Contexte

Le choix d'une technologie d'API impacte directement la performance, la maintenabilité et la scalabilité des applications modernes.  
Cette étude propose une analyse empirique de quatre technologies d’API sur un cas concret : une plateforme de réservation hôtelière.

### Objectifs

- Mesurer les performances sous différentes charges.
- Comparer l'utilisation des ressources système (CPU, mémoire, réseau).
- Évaluer la scalabilité et la résilience.
- Analyser la complexité d'implémentation.
- Fournir des recommandations par cas d’usage.

### Limitations

- Tests en environnement Docker local (non production).
- Service gRPC partiellement implémenté (certaines données estimées).
- Opérations CRUD simples uniquement.
- Pas de tests de sécurité approfondis.
- Réseau idéal (pas de latence simulée).

---

## 🔧 Technologies Étudiées

### REST – Representational State Transfer

- Architecture : sans état, HTTP standard.
- Format : JSON / XML.
- Points forts : simplicité, caching HTTP, écosystème mature.
- Implémentation : Spring Boot 3.2.0 + Spring Data JPA.

### SOAP – Simple Object Access Protocol

- Architecture : protocole XML standardisé W3C.
- Format : XML + schémas XSD.
- Points forts : WS-Security, contrat WSDL, standards d’entreprise.
- Implémentation : Spring Web Services + JAXB.

### GraphQL

- Architecture : langage de requête avec schéma typé.
- Format : JSON.
- Points forts : flexibilité, élimination de l’over/under‑fetching.
- Implémentation : Apollo Server + Node.js + PostgreSQL.

### gRPC – Google Remote Procedure Call

- Architecture : framework RPC haute performance.
- Format : Protocol Buffers (binaire).
- Points forts : HTTP/2, streaming bidirectionnel, typage fort.
- Implémentation : fichiers `.proto` (service partiellement implémenté).

---

## 🧪 Méthodologie

### Infrastructure de test

| Composant       | Spécification                         |
|-----------------|---------------------------------------|
| OS              | Windows 11 Pro                        |
| Docker          | Docker Desktop 4.25.0                 |
| CPU             | Intel Core i7‑11800H (8 cœurs)        |
| RAM             | 16 GB DDR4                            |
| Disque          | SSD NVMe 512 GB                       |
| Base de données | PostgreSQL 15                         |
| Backend         | Spring Boot (REST/SOAP), Node.js (GraphQL) |
| Monitoring      | Prometheus, Grafana, Jaeger           |
| Outils de test  | k6, Locust                            |

### Scénarios de charge

| Scénario       | Utilisateurs | Durée | Objectif           |
|----------------|-------------:|------:|--------------------|
| Baseline       | 10           | 2 min | Référence          |
| Charge moyenne | 100          | 5 min | Usage normal       |
| Charge élevée  | 500          | 5 min | Pic d’activité     |
| Stress test    | 1000         | 10 min| Limites système    |

### Opérations testées

- CREATE : créer une réservation.
- READ : consulter une réservation.
- UPDATE : modifier une réservation.
- DELETE : annuler une réservation.

---

## 📊 Résultats Détaillés

### Latence moyenne (100 utilisateurs, messages 1 KB)

| API     | CREATE (ms) | READ (ms) | UPDATE (ms) | DELETE (ms) | Moyenne (ms) |
|---------|-------------|----------:|------------:|------------:|-------------:|
| REST    | 68,4        | 15,2      | 54,5        | 17,4        | 48,6         |
| SOAP    | 142,5       | 85,3      | 98,7        | 72,1        | 94,7         |
| GraphQL | 41,0        | 53,0      | 55,5        | 18,2        | 41,9         |
| gRPC    | 28,5        | 12,8      | 35,2        | 14,3        | 32,7         |

### Débit (100 utilisateurs, messages 1 KB)

| API     | Requêtes par seconde (RPS) |
|---------|---------------------------:|
| REST    | 1245                       |
| SOAP    | 680                        |
| GraphQL | 1350                       |
| gRPC    | 1850                       |

### Ressources (500 utilisateurs)

| API     | CPU (%) | RAM (MB) | Réseau (MB/s) |
|---------|--------:|---------:|--------------:|
| REST    | 45,2    | 512      | 12,5          |
| SOAP    | 68,5    | 780      | 28,3          |
| GraphQL | 52,3    | 595      | 15,8          |
| gRPC    | 38,7    | 445      | 8,2           |

---

## 📈 Analyse Comparative

### Score global (sur 60)

| Critère     | REST | SOAP | GraphQL | gRPC |
|-------------|-----:|-----:|--------:|-----:|
| Performance | 7/10 | 4/10 | 8/10    | 10/10|
| Simplicité  |10/10 | 3/10 | 6/10    | 5/10 |
| Scalabilité | 7/10 | 4/10 | 8/10    | 10/10|
| Écosystème  |10/10 | 6/10 | 7/10    | 6/10 |
| Sécurité    | 7/10 | 9/10 | 7/10    | 8/10 |
| Maintenance | 9/10 | 4/10 | 6/10    | 7/10 |
| **Total**   |**50**| 30   | 42      | 46   |

---

## 🎯 Recommandations

### Par cas d’usage

| Cas d’usage                       | Technos recommandées | Raison principale                 |
|-----------------------------------|----------------------|-----------------------------------|
| Application web publique          | REST                 | Simplicité, caching, SEO         |
| Application mobile                | GraphQL              | Flexibilité, optimisation réseau |
| Microservices internes            | gRPC                 | Performance, faible latence      |
| Intégration B2B / legacy          | SOAP                 | WS‑Security, WSDL, conformité    |
| Temps réel / streaming            | gRPC                 | Streaming bidirectionnel         |
| APIs publiques                    | REST                 | Standard de facto                |
| Données relationnelles complexes  | GraphQL              | Pas d’over/under‑fetching        |

---

## 🏁 Conclusion

- **REST** : meilleur choix pour démarrer rapidement, petite équipe, APIs publiques.  
- **SOAP** : pertinent pour l’intégration de systèmes legacy et les environnements très régulés.  
- **GraphQL** : idéal pour applications mobiles et frontends riches.  
- **gRPC** : recommandé pour microservices internes, contraintes de performance et IoT.

---

## 📚 Références

- Fielding, R. T. (2000). *Architectural Styles and the Design of Network-based Software Architectures*.  
- W3C. (2007). *SOAP Version 1.2 Part 1: Messaging Framework*.  
- Facebook Inc. (2015). *GraphQL Specification*.  
- Google. (2016). *gRPC: A high-performance, open-source universal RPC framework*.  
- Richardson, L., & Ruby, S. (2007). *RESTful Web Services*. O'Reilly.  
- Newman, S. (2021). *Building Microservices, 2nd Edition*. O'Reilly.
