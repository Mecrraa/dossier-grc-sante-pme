# Politique de Sécurité du Système d'Information (PSSI)
**Organisation :** Résidence « Les Jardins d'Ambre » - **Référentiel :** ANSSI / ISO 27001:2022

## 1. Objectifs et Périmètre
Garantir la disponibilité 24/7 du système d'appel d'urgence, la confidentialité des dossiers médicaux/résidents, et la résilience face aux rançongiciels pour l'ensemble des 35 salariés et des prestataires externes.

## 2. Règles de Sécurité Opérationnelles
- **IAM-01 & 02 (Comptes & MFA) :** Comptes nominatifs obligatoires. Mots de passe de 14 caractères minimum. Authentification multifacteur (MFA) exigée sur Microsoft 365, le SaaS `RésidGest` et le VPN.
- **IAM-03 & 04 (Moindre privilège) :** Pas de droits admin locaux sur les postes (gestion par Windows LAPS). Révocation immédiate des accès en cas de départ (offboarding).
- **NET-01 & 02 (Segmentation VLAN) :** Cloisonnement strict en 4 VLANs : `VLAN 10` (Serveurs), `VLAN 20` (Bureautique), `VLAN 30` (IoT / Appel malade - sans accès Internet direct), `VLAN 40` (Wi-Fi Invités isolé). Désactivation des protocoles obsolètes (SMBv1, HTTP non sécurisé).
- **END-01 à 03 (Postes & Mobilité) :** Verrouillage auto après 5 min, chiffrement BitLocker, blocage des macros Office et interdiction des clés USB personnelles.
- **TRD-01 à 03 (Gestion des tiers) :** Interdiction des logiciels de prise en main non maîtrisés (TeamViewer permanent). Accès des prestataires (`InfoProx`, `DomoSecur`) restreints à un VPN nominatif sécurisé par MFA.
- **BCP-01 & 02 (Sauvegardes & PRA) :** Règle de sauvegarde 3-2-1-1-0 (NAS immuable hors domaine + Cloud chiffré). Test de restauration trimestriel (RTO ciblé à 2h pour l'appel malade).
- **SOC-01 (Supervision) :** Centralisation des journaux (Windows EventLogs, Sysmon, Pare-feu) sur le SIEM **Wazuh** avec alertes sur les comportements suspects (force brute, élévation de privilèges).
