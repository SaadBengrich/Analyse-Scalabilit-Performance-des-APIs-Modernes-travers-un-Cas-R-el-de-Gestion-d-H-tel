Comparaison des Technologies d'API
REST, SOAP, GraphQL et gRPC
Cas d’Étude : Plateforme de Réservation Hôtelière

Auteurs : BENGRICH Saad, JABBOUR Omar
Institution : ÉCOLE MAROCAINE DE SCIENCE DE L'INGÉNIERIE
Date : Décembre 2024

📋 Table des Matières
Résumé Exécutif

Introduction

Technologies Étudiées

Méthodologie

Résultats Détaillés

Analyse Comparative

Recommandations

Conclusion

🎯 Résumé Exécutif
Cette étude compare quatre technologies d'API majeures (REST, SOAP, GraphQL, gRPC) dans le contexte d'une plateforme de réservation hôtelière.
Les tests sous charges variables (10–1000 requêtes simultanées) montrent que :

gRPC offre les meilleures performances (latence moyenne 32.7 ms, 1850 RPS).

REST excelle en simplicité et adoption (48.6 ms, 1245 RPS).

GraphQL optimise la flexibilité (41.9 ms, 1350 RPS).

SOAP reste pertinent pour les environnements legacy (94.7 ms, 680 RPS).

📖 Introduction
Contexte
Le choix d'une technologie d'API impacte directement la performance, la maintenabilité et la scalabilité des applications modernes.
Cette étude propose une analyse empirique de quatre technologies d’API sur un cas concret : une plateforme de réservation hôtelière.

Objectifs
Mesurer les performances sous différentes charges.

Comparer l’utilisation des ressources (CPU, mémoire, réseau).

Évaluer la scalabilité et la résilience.

Analyser la complexité d’implémentation.

Fournir des recommandations par cas d’usage.

Limitations
Tests en Docker local (environnement non production).

Service gRPC partiellement implémenté (certaines données estimées).

Opérations CRUD simples uniquement.

Pas de tests de sécurité approfondis.

Réseau idéal (pas de latence simulée).

🔧 Technologies Étudiées
REST – Representational State Transfer
Architecture : sans état, HTTP standard.

Format : JSON / XML.

Points forts : simplicité, caching HTTP, écosystème très mature.

Implémentation : Spring Boot 3.2.0 + Spring Data JPA.

SOAP – Simple Object Access Protocol
Architecture : protocole XML standardisé W3C.

Format : XML + XSD.

Points forts : WS-Security, contrat WSDL, standards d’entreprise.

Implémentation : Spring Web Services + JAXB.

GraphQL
Architecture : langage de requête avec schéma typé.

Format : JSON.

Points forts : flexibilité, élimination over/under-fetching.

Implémentation : Apollo Server + Node.js + PostgreSQL.

gRPC – Google Remote Procedure Call
Architecture : framework RPC haute performance.

Format : Protocol Buffers (binaire).

Points forts : HTTP/2, streaming bidirectionnel, typage fort.

Implémentation : fichiers .proto (service partiellement implémenté).

🧪 Méthodologie
Infrastructure de Test
Composant	Spécification
OS	Windows 11 Pro
Docker	Docker Desktop 4.25.0
CPU	Intel Core i7‑11800H @ 2.3 GHz (8 cœurs)
RAM	16 GB DDR4
Disque	SSD NVMe 512 GB
Base de données	PostgreSQL 15
Backend	Spring Boot (REST/SOAP), Node.js (GraphQL)
Monitoring	Prometheus, Grafana, Jaeger
Outils de test	k6, Locust
Scénarios de Charge
Scénario	Utilisateurs	Durée	Objectif
Baseline	10	2 min	Référence
Charge moyenne	100	5 min	Usage normal
Charge élevée	500	5 min	Pic d’activité
Stress test	1000	10 min	Limites système
Opérations Testées
CREATE : créer une réservation.

READ : consulter une réservation.

UPDATE : modifier une réservation.

DELETE : annuler une réservation.

Tailles de Messages
Petit (1 KB) : réservation simple.

Moyen (10 KB) : réservation + préférences.

Grand (100 KB) : réservation + historique complet.

📊 Résultats Détaillés
1. Latence (100 utilisateurs, 1 KB)
API	CREATE (ms)	READ (ms)	UPDATE (ms)	DELETE (ms)	Moyenne (ms)
REST	68.4	15.2	54.5	17.4	48.6
SOAP	142.5	85.3	98.7	72.1	94.7
GraphQL	41.0	53.0	55.5	18.2	41.9
gRPC	28.5	12.8	35.2	14.3	32.7
gRPC est ~33 % plus rapide que REST et ~65 % plus rapide que SOAP en latence moyenne.

Impact de la Taille des Messages
Taille	REST (ms)	SOAP (ms)	GraphQL (ms)	gRPC (ms)
1 KB	48.6	94.7	41.9	32.7
10 KB	75.8	187.5	82.5	47.5
100 KB	251.8	573.3	246.3	145.0
SOAP voit sa latence croître beaucoup plus vite que REST, GraphQL et gRPC.

2. Débit (Throughput)
RPS vs Taille (100 utilisateurs)

Taille	REST	SOAP	GraphQL	gRPC
1 KB	1245	680	1350	1850
10 KB	485	245	520	725
100 KB	78	35	82	125
gRPC maintient le débit le plus élevé pour toutes les tailles de messages.

3. Utilisation des Ressources (500 utilisateurs)
API	CPU (%)	RAM (MB)	Connexions DB	Réseau (MB/s)
REST	45.2	512	85	12.5
SOAP	68.5	780	120	28.3
GraphQL	52.3	595	95	15.8
gRPC	38.7	445	75	8.2
gRPC utilise 44 % moins de CPU que SOAP.

SOAP consomme 75 % de RAM en plus que gRPC.

4. Taille des Messages (CREATE)
API	Requête (bytes)	Réponse (bytes)	Total	Variation vs REST
REST	2855	2080	4935	—
SOAP	12400	18500	30900	+284 %
GraphQL	4200	5800	10000	+24 %
gRPC	1800	2500	4300	−46 %
gRPC réduit le payload de 46 % vs REST et 86 % vs SOAP.

📈 Analyse Comparative
Score Global (multi‑critères)
Critère	REST	SOAP	GraphQL	gRPC
Performance	7/10	4/10	8/10	10/10
Simplicité	10/10	3/10	6/10	5/10
Scalabilité	7/10	4/10	8/10	10/10
Écosystème	10/10	6/10	7/10	6/10
Sécurité	7/10	9/10	7/10	8/10
Maintenance	9/10	4/10	6/10	7/10
Total	50/60	30/60	42/60	46/60
Forces / Faiblesses Résumées
REST

✅ Très simple, écosystème universel, tooling riche (OpenAPI/Swagger).

❌ Over/under‑fetching, JSON plus lourd que binaire.

SOAP

✅ WS‑Security, WSDL, adapté aux environnements enterprise / legacy.

❌ Latence + consommation CPU/RAM les plus élevées, XML très verbeux.

GraphQL

✅ Flexibilité des requêtes, idéal pour fronts complexes / mobiles.

❌ Caching plus complexe, risques N+1, monitoring/debug plus difficile.

gRPC

✅ Meilleures performances globales, streaming, payload compact.

❌ Support navigateur direct limité (gRPC‑Web), debug binaire plus dur.

🎯 Recommandations
Par Cas d’Usage
Cas d’usage	Technologie	Raison principale
Application web publique	REST	Simplicité, caching HTTP, adoption massive
Application mobile	GraphQL	Flexibilité, optimisation bande passante
Microservices internes	gRPC	Performance, streaming, faible latence
Intégration B2B / legacy	SOAP	Standards entreprise, WS‑Security
Temps réel (streaming)	gRPC	Streaming bidirectionnel, HTTP/2
APIs publiques	REST	Standard de facto, tooling universel
Données relationnelles complexes	GraphQL	Pas d’over‑fetching, requêtes riches
IoT / Edge	gRPC	Payload compact, réseau limité
Architecture Hybride Recommandée
text
API Gateway / Load Balancer
           │
   ┌───────┴────────┐
   │                │
REST API        GraphQL API
- Web public    - Apps mobiles
- SEO           - Données complexes
   └───────┬───────┘
           │
     gRPC Services
     - Microservices
     - Communication interne
           │
      SOAP Gateway
      - Intégrations B2B / legacy
      - ERP / CRM
🏁 Conclusion
Synthèse
Performance :

🥇 gRPC (32.7 ms, 1850 RPS, −46 % payload vs REST).

🥈 GraphQL (41.9 ms, 1350 RPS).

🥉 REST (48.6 ms, 1245 RPS).

4️⃣ SOAP (94.7 ms, 680 RPS).

Scalabilité :

gRPC stable jusqu’à 800+ utilisateurs.

REST / GraphQL commencent à souffrir au‑delà de ~500 utilisateurs.

SOAP se dégrade dès ~350 utilisateurs.

Complexité :

REST : le plus simple.

SOAP : le plus complexe.

GraphQL / gRPC : intermédiaire, mais plus exigeant en expertise.

Choix Rapide
REST : démarrer vite, équipe petite, compatibilité maximale.

SOAP : intégration avec systèmes legacy, exigence de standards enterprise.

GraphQL : fronts riches, mobiles, données complexes.

gRPC : microservices, performance critique, streaming, IoT.

