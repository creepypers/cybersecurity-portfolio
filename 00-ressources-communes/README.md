# 00 — Ressources communes

Ce module centralise les éléments réutilisables par tous les scénarios du portfolio.

## Objectif
- Uniformiser la qualité des livrables
- Réduire la duplication documentaire
- Faciliter la traçabilité des preuves

## Structure
- `modeles/` : modèles de documents (registre, rapport, plan d’action, playbook)
- `references/` : référentiels, guides réglementaires, normes, sources techniques

## Règles d’utilisation
1. Chaque nouveau module doit réutiliser les modèles de `modeles/` avant de créer un nouveau format.
2. Les références externes doivent être citées avec date d’accès.
3. Les artefacts sensibles doivent être anonymisés avant dépôt.

## Livrables attendus
- Templates versionnés
- Bibliothèque de références classées (GRC, IAM, Réseau, IR, Automatisation)
- Convention de nommage partagée

## Contrôles qualité
- Cohérence de format entre modules
- Références vérifiables
- Absence de données sensibles
