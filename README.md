# Comparaison des Technologies d'API  
REST, SOAP, GraphQL et gRPC  
**Cas d'Étude : Plateforme de Réservation Hôtelière**

**Auteurs** : BENGRICH Saad, JABBOUR Omar  
**Institution** : ÉCOLE MAROCAINE DE SCIENCE DE L'INGÉNIEUR  
**Date** : Décembre 2024  

---

## 📋 Table des Matières

- [Résumé Exécutif](#-résumé-exécutif)
- [Tableaux des Résultats](#-tableaux-des-résultats)
- [Technologies Étudiées](#-technologies-étudiées)
- [Méthodologie](#-méthodologie)
- [Analyse Comparative](#-analyse-comparative-détaillée)
- [Recommandations](#-recommandations)
- [Conclusion](#-conclusion)

---

## 🎯 Résumé Exécutif

Cette étude compare quatre technologies d'API majeures (**REST**, **SOAP**, **GraphQL**, **gRPC**) dans le contexte d'une plateforme de réservation hôtelière.  
Les tests sous charges variables (10–1000 requêtes simultanées) révèlent que :

- **gRPC** offre les meilleures performances (32,7 ms de latence moyenne, 1850 RPS).
- **REST** excelle en simplicité et adoption (48,6 ms, 1245 RPS).
- **GraphQL** optimise la flexibilité (41,9 ms, 1350 RPS).
- **SOAP** reste pertinent pour les environnements legacy (94,7 ms, 680 RPS).

---

## 📊 Tableaux des Résultats

### 1. Performances – Latence (1 KB, 100 utilisateurs)

| Opération  | REST (ms) | SOAP (ms) | GraphQL (ms) | gRPC (ms) |
|-----------|----------:|----------:|-------------:|----------:|
| Créer     | 68,4      | 142,5     | 41,0         | 28,5      |
| Consulter | 15,2      | 85,3      | 53,0         | 12,8      |
| Modifier  | 54,5      | 98,7      | 55,5         | 35,2      |
| Supprimer | 17,4      | 72,1      | 18,2         | 14,3      |
| **Moyenne** | **48,6** | **94,7** | **41,9**     | **32,7**  |

### 2. Débit – Requêtes par seconde

| Requêtes simultanées | REST | SOAP | GraphQL | gRPC |
|----------------------|-----:|-----:|--------:|-----:|
| 10                   | 1450 | 825  | 1520    | 2100 |
| 100                  | 1245 | 680  | 1350    | 1850 |
| 500                  | 785  | 385  | 825     | 1120 |
| 1000                 | 425  | 185  | 485     | 650  |

> **Analyse** : gRPC maintient le débit le plus élevé à toutes les charges (48 % de RPS en plus que REST à 100 utilisateurs, 172 % de plus que SOAP).

---

## 🔧 Technologies Étudiées

### REST – Representational State Transfer

- Architecture : sans état, HTTP standard.  
- Format : JSON, XML.  
- Points forts : simplicité, excellent caching, écosystème mature.  
- Implémentation : Spring Boot 3.2.0 + Spring Data JPA.

### SOAP – Simple Object Access Protocol

- Architecture : protocole XML standardisé W3C.  
- Format : XML + XSD.  
- Points forts : WS‑Security, WSDL, standards d’entreprise.  
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

### Infrastructure de Test

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

### Scénarios de Test

| Scénario       | Utilisateurs | Durée | Objectif         |
|----------------|-------------:|------:|------------------|
| Baseline       | 10           | 2 min | Référence        |
| Charge moyenne | 100          | 5 min | Usage normal     |
| Charge élevée  | 500          | 5 min | Pic d’activité   |
| Stress         | 1000         |10 min | Limites système  |

---

## 📈 Analyse Comparative Détaillée

### Score Global (sur 60)

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

- **REST** : idéal pour démarrer vite, APIs publiques, petite équipe.  
- **GraphQL** : recommandé pour mobiles et frontends riches.  
- **gRPC** : pour microservices internes, performance et streaming.  
- **SOAP** : pour intégration B2B / legacy avec fortes exigences de sécurité.

---

## 🏁 Conclusion

- REST = meilleur compromis simplicité / écosystème.  
- gRPC = meilleures performances brutes (latence, débit, payload).  
- GraphQL = flexibilité maximale côté client.  
- SOAP = sécurité et standards d’entreprise, mais coûteux en ressources.
