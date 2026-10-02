# Portfolio Professionnel Cybersécurité

**Architecte Sécurité & Ingénieur Cybersécurité Junior+ (orientation Analyste Cybersécurité / GRC / SOC)**

Ce dépôt présente un **portfolio monorepo** structuré pour démontrer des compétences techniques et méthodologiques couvrant les domaines clés attendus en cybersécurité opérationnelle et gouvernance.

**Profil & trajectoire :**
- Titulaire du **Google Cybersecurity Certificate (GCC)**
- Préparation active de **CompTIA Security+ (SY0-701)**
- Positionnement cible : **Analyste Cybersécurité / GRC / SOC Junior**

---

## Arborescence proposée (Monorepo)

```text
.
├── 00-ressources-communes/
│   ├── modeles/
│   ├── references/
│   └── README.md
├── 01-gouvernance-risques-conformite/
│   ├── registres-risques/
│   ├── audits/
│   ├── conformite-normative/
│   └── README.md
├── 02-iam-controle-acces/
│   ├── matrices-rbac/
│   ├── revues-acces/
│   ├── politiques-iam/
│   └── README.md
├── 03-securite-reseau-analyse-trafic/
│   ├── pcap/
│   ├── analyses-wireshark/
│   ├── regles-pare-feu/
│   ├── segmentation/
│   └── README.md
├── 04-automatisation-admin-systeme/
│   ├── scripts-python/
│   ├── hardening-linux/
│   ├── outils-bash/
│   └── README.md
└── 05-detection-menaces-reponse-incidents/
    ├── analyses-siem/
    ├── playbooks/
    ├── gestion-artefacts/
    └── README.md
```

---

## Matrice de compétences techniques et réglementaires

| Domaine | Frameworks / Référentiels | Outils & Plateformes | Langages / Scripting |
|---|---|---|---|
| GRC | NIST CSF v2.0, ISO 27001, Loi 25, RGPD | Registres de risques, matrices de conformité, checklists d’audit | Markdown, CSV |
| IAM | Principes Zero Trust, RBAC, moindre privilège | IAM policy review, revues d’accès, matrices d’habilitation | Bash, Python |
| Sécurité Réseau | Défense en profondeur, segmentation, ACL | Wireshark, tcpdump, règles pare-feu | Bash |
| Automatisation & Système | Hardening guides, baseline sécurité Linux | Linux CLI, scripts d’automatisation sécurité | Python, Bash |
| Détection & IR | MITRE ATT&CK (mapping), cycle IR | SIEM (requêtes/logs), playbooks, gestion d’artefacts | Python, Bash, KQL/SPL (selon SIEM) |

---

## Index des modules du portfolio

| Module | Objectif technique | Compétences clés validées | Lien |
|---|---|---|---|
| 01 - Gouvernance, Risques & Conformité | Concevoir des livrables GRC exploitables (risques, contrôles, conformité) | Identification des risques, plan de traitement, auditabilité, mapping réglementaire | [01-gouvernance-risques-conformite](./01-gouvernance-risques-conformite/) |
| 02 - IAM & Contrôle d’accès | Implémenter une gestion d’accès robuste basée sur le moindre privilège | RBAC, revues d’accès, gouvernance des identités, séparation des rôles | [02-iam-controle-acces](./02-iam-controle-acces/) |
| 03 - Sécurité Réseau & Analyse de trafic | Analyser des flux réseau et proposer des mesures de protection | Analyse PCAP, détection d’anomalies, filtrage réseau, segmentation | [03-securite-reseau-analyse-trafic](./03-securite-reseau-analyse-trafic/) |
| 04 - Automatisation & Administration Système | Développer des scripts orientés sécurité et opérations Linux | Automatisation défensive, collecte d’indices, durcissement système, CLI avancée | [04-automatisation-admin-systeme](./04-automatisation-admin-systeme/) |
| 05 - Détection, Menaces & Réponse aux incidents | Simuler et documenter la détection et la réponse à incidents | Triage alertes, investigation logs, playbooks IR, chaîne de preuve | [05-detection-menaces-reponse-incidents](./05-detection-menaces-reponse-incidents/) |

---

## Méthodologie de documentation et validation

Chaque scénario est documenté de manière reproductible avec :
1. **Contexte & objectif** (menace, périmètre, hypothèses)
2. **Procédure technique** (étapes, commandes, règles, scripts)
3. **Preuves & artefacts** (captures, logs, extraits anonymisés)
4. **Résultats & analyse** (constats, risques résiduels, priorisation)
5. **Plan d’amélioration** (correctifs, métriques de suivi, revalidation)

La validation croise systématiquement les exigences de conformité, l’applicabilité opérationnelle et la traçabilité des décisions.

---

## Commandes Bash rapides (création de structure + fichiers vides)

```bash
mkdir -p \
  00-ressources-communes/{modeles,references} \
  01-gouvernance-risques-conformite/{registres-risques,audits,conformite-normative} \
  02-iam-controle-acces/{matrices-rbac,revues-acces,politiques-iam} \
  03-securite-reseau-analyse-trafic/{pcap,analyses-wireshark,regles-pare-feu,segmentation} \
  04-automatisation-admin-systeme/{scripts-python,hardening-linux,outils-bash} \
  05-detection-menaces-reponse-incidents/{analyses-siem,playbooks,gestion-artefacts}

touch \
  00-ressources-communes/README.md \
  01-gouvernance-risques-conformite/README.md \
  02-iam-controle-acces/README.md \
  03-securite-reseau-analyse-trafic/README.md \
  04-automatisation-admin-systeme/README.md \
  05-detection-menaces-reponse-incidents/README.md
```
