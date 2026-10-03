# Registre des Actifs & Classification de Sécurité (CIA & Loi 25)

**Organisation :** Novapay Solutions Inc.  
**Cadre de référence :** ISO/IEC 27001:2022 | Loi 25 (Québec) | NIST CSF v2.0  
**Statut :** Approuvé  
**Dernière révision :** Octobre 2026  

---

## 1. Matrice de Classification des Actifs de Sécurité

| ID Actif | Nom de l'actif | Catégorie d'actif | Propriétaire (Asset Owner) | Dépositaire (Asset Custodian) | C | I | A | Justification d'affaires & d'impact (C-I-A) | Nature des données (Loi 25) | Exigences réglementaires clés (Loi 25) |
| :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- |
| **FR-001** | Application Web & Mobile (Frontend React) | Logiciel / Application client web | **VP Engineering / CTO** | Équipe Développement Frontend | **Moyen** | **Critique** | **Élevé** | **C :** Le code compilé est public côté client mais expose la logique d'appel API.<br>**I :** Une injection malveillante (XSS / Magecart) intercepte les identifiants et données bancaires à la source.<br>**A :** Vitrine commerciale et point d'accès unique des clients ; une panne bloque l'expérience utilisateur. | RPS en transit / collecte | **Art. 9.1** (Confidentialité par défaut)<br>**Art. 10** (Sécurisation du canal de collecte)<br>**Art. 12** (Minimisation et interdiction de mise en cache locale non sécurisée) |
| **BK-001** | Moteurs de calcul & API Métier (.NET / Python) | Logiciel / Services applicatifs Backend | **VP Engineering / CTO** | Équipe Développement Backend & DevOps | **Critique** | **Critique** | **Critique** | **C :** Fait transiter des données bancaires déchiffrées en mémoire vive et contient les secrets d'API partenaires.<br>**I :** Une altération de la logique métier entraîne des transferts frauduleux ou des calculs de crédit erronés.<br>**A :** Point névralgique de traitement ; son arrêt stoppe immédiatement l'ensemble des transactions de l'entreprise. | RPS en transit / traitement | **Art. 10** (Mesures de sécurité techniques et organisationnelles proportionnées)<br>**Art. 17** (ÉFVP obligatoire pour tout flux transfrontalier ou sous-traitance logicielle) |
| **BD-001** | Base de données de production (RDS PostgreSQL) | Données / Base de données relationnelle | **Chief Data Officer (CDO)** *(ou VP Data)* | Administrateur Base de Données (DBA) / Cloud Engineer | **Critique** | **Critique** | **Critique** | **C :** Héberge l'historique complet des clients, NAS, coordonnées bancaires et pièces KYC.<br>**I :** La corruption des enregistrements financiers détruit l'intégrité comptable et juridique de la FinTech.<br>**A :** Indisponibilité = incapacité totale d'opérer, non-respect des engagements contractuels et perte de licence. | RPS au repos | **Art. 3.3 & 17** (ÉFVP pour le stockage de données sensibles en infonuagique)<br>**Art. 8** (Consentement exprès obligatoire pour RPS)<br>**Art. 10** (Chiffrement at-rest et contrôle d'accès strict)<br>**Art. 23** (Conservation limitée, destruction ou anonymisation irréversible) |
| **OST-002** | Compartiment de sauvegardes (AWS S3) | Infrastructure & Données / Stockage d'objets Cloud | **Chief Data Officer (CDO)** | Infrastructure Cloud Lead / DevOps | **Critique** | **Critique** | **Critique** | **C :** Contient l'image miroir complète de la production sous forme d'archives non chiffrées.<br>**I :** L'altération ou le chiffrement par un ransomware empêche toute restauration intègre du système.<br>**A :** Dernier rempart de résilience opérationnelle ; conditionne directement le RTO (délai maximal admissible de reprise). | RPS au repos (Sauvegardes) | **Art. 10** (Chiffrement robuste géré par le client, immuabilité des sauvegardes)<br>**Art. 23** (Application automatisée des politiques d'épuration et de rétention légale) |
| **CMP-001** | Postes de travail collaborateurs (macOS) | Matériel / Terminaux utilisateurs (Endpoints) | **IT Operations Lead** | Administrateur Systèmes TI / Support TI | **Élevé** | **Élevé** | **Moyen** | **C :** Points d'entrée en 100 % télétravail ; contiennent des sessions actives et des clés d'accès aux infrastructures de production.<br>**I :** La compromission d'un poste permet l'usurpation d'identité et l'injection de code dans les dépôts sources.<br>**A :** La perte d'un terminal handicape un employé mais ne bloque pas la disponibilité globale des services de la FinTech. | RP / RPS accédés | **Art. 10** (Chiffrement obligatoire des disques, MDM centralisé, EDR)<br>**Art. 3.5 & 3.8** (Signalement immédiat de perte/vol et inscription au registre des incidents) |

---

## 2. Constats d'Audit Préliminaires (Non-Conformités Majeures)

### NC-01 — Absence d'immuabilité et de chiffrement dédié des sauvegardes
* **Sévérité :** Critique
* **Référentiels impactés :** ISO/IEC 27001:2022 (A.8.13 - Sauvegarde des données, A.8.24 - Utilisation de la cryptographie) | Loi 25 (Art. 10)
* **Constat factuel :** Les sauvegardes quotidiennes de la base de données PostgreSQL sont synchronisées dans un compartiment AWS S3 sans clé de chiffrement dédiée (KMS CMK) et sans activation de la protection contre la suppression ou modification (S3 Object Lock en mode conformité).
* **Risque d'affaires & légal :** En cas d'attaque par ransomware ou de compromission de compte Cloud, les sauvegardes peuvent être détruites ou chiffrées simultanément avec la production, provoquant une perte définitive d'actifs critiques et une incapacité totale de reprise d'activité.

### NC-02 — Non-respect du principe de moindre privilège et défaut de séparation des tâches (SoD)
* **Sévérité :** Critique
* **Référentiels impactés :** ISO/IEC 27001:2022 (A.5.3 - Séparation des tâches, A.8.2 - Droits d'accès privilégiés, A.8.18 - Gestion des accès aux privilèges) | Loi 25 (Art. 10)
* **Constat factuel :** L'ensemble des développeurs détient des accès directs en lecture et en écriture sur la base de données RDS PostgreSQL de production sans passerelle d'accès sécurisée (bastion PAM), sans authentification multifacteur (MFA) imposée et sans journalisation granulaire des requêtes SQL exécutées.
* **Risque d'affaires & légal :** Risque direct de fraude interne, de fuite massive de renseignements personnels sensibles (NAS, soldes, pièces KYC) et d'altération accidentelle des données de production sans imputabilité possible (violation du principe de non-répudiation).

### NC-03 — Manque de gouvernance formelle et défaut d'encadrement réglementaire
* **Sévérité :** Majeure
* **Référentiels impactés :** Loi 25 (Art. 3.1 - Désignation du RPRP, Art. 3.5 à 3.8 - Gestion et registre des incidents de confidentialité) | ISO/IEC 27001:2022 (A.5.1 - Politiques de sécurité, A.5.2 - Rôles et responsabilités)
* **Constat factuel :** Aucun Responsable de la protection des renseignements personnels (RPRP) n'est formellement mandaté par écrit, aucun registre des incidents de confidentialité n'est opérationnel et aucune solution centralisée de surveillance/journalisation n'est déployée.
* **Risque d'affaires & légal :** Incapacité légale de détecter, évaluer et notifier un incident présentant un risque de préjudice sérieux à la Commission d'accès à l'information (CAI) dans les délais prescrits, exposant Novapay à des sanctions administratives et pénales pouvant atteindre 25 000 000 $ CAD ou 4 % du chiffre d'affaires mondial.