# Scénario 1 — Évaluation des Risques & Conformité Loi 25 (FinTech B2B/B2C)

## Contexte de l'organisation
**Novapay Solutions** est une FinTech québécoise basée à Québec qui commercialise une plateforme SaaS de micro-prêts et d'agrégation de comptes bancaires pour particuliers et commerçants.

### Environnement technique & opérationnel
* **Architecture applicative** : Approche API-first (frontend React, backends .NET Core et Python) hébergée sur AWS (EKS, RDS PostgreSQL, buckets S3).
* **Données manipulées** : Renseignements personnels et bancaires (spécimens de chèques, numéros d'assurance sociale (NAS), états de compte, soldes via API bancaires tierces, pièces d'identité scannées pour le KYC).
* **Effectif & mode de travail** : 45 employés, 100 % en télétravail ou formule hybride, utilisant des postes macOS gérés sommairement (sans solution MDM centralisée).
* **Historique récent & gouvernance** : Croissance rapide sans RSSI/CISO dédié jusqu'à maintenant. Les développeurs disposent d'accès directs en lecture/écriture à la base de données RDS de production pour corriger les incidents. Les sauvegardes PostgreSQL sont synchronisées quotidiennement dans un bucket S3 sans chiffrement KMS dédié ni verrouillage d'objet (*S3 Object Lock*).

---

## Tâche 1 : Cartographie des Actifs & Classification de Sécurité

### Objectif
Établir une matrice d'inventaire et de classification de sécurité alignée sur les standards de gouvernance (ISO/IEC 27001) et les exigences de la Loi 25 québécoise (Loi P-39.1).

### Consignes de rédaction
1. **Identification des actifs** : Sélectionner 4 à 5 actifs critiques représentatifs du périmètre technologique et opérationnel.
2. **Évaluation CIA (Confidentialité, Intégrité, Disponibilité)** :
   * Attribuer une cote (*Faible*, *Moyen*, *Élevé*, *Critique*) pour chaque dimension.
   * Fournir une justification d'affaires ou d'impact technique pour chaque actif.
3. **Classification Loi 25 (Québec)** :
   * Préciser la nature des données : *Aucune*, *RP* (Renseignements Personnels) ou *RPS* (Renseignements Personnels Sensibles), au repos ou en transit.
   * Associer les obligations légales majeures (ex. Art. 3.1, Art. 8, Art. 9.1, Art. 10, Art. 17, Art. 23).
4. **Attribution de la gouvernance** :
   * Désigner le propriétaire formel de l'actif (**Asset Owner**) selon la séparation des rôles (respecter la deuxième ligne de défense du CISO).
   * Identifier le dépositaire technique (**Asset Custodian**).
5. **Constats d'audit préliminaires** :
   * Rédiger 3 constats majeurs formulés selon la terminologie formelle d'audit (Constat / Risque opérationnel & réglementaire).

---

### Structure attendue du tableau

| ID Actif | Nom de l'actif | Catégorie | Propriétaire (Asset Owner) | Dépositaire (Asset Custodian) | C | I | A | Justification d'affaires & d'impact | Nature des données (Loi 25) | Exigences réglementaires clés (Loi 25) |
| :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: | :--- | :--- | :--- |
| `ID` | `Nom` | `Catégorie` | `Owner` | `Custodian` | `C` | `I` | `A` | `Justification` | `RP / RPS` | `Articles applicables` |