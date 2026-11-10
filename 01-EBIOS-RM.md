# Analyse de Risques EBIOS RM - Résidence « Les Jardins d'Ambre »

## 1. Contexte et Périmètre
- **Structure :** Résidence services seniors de 80 résidents et 35 salariés.
- **SI Actuel :** Réseau plat (`192.168.1.0/24`), 1 serveur physique (Hyper-V avec `SRV-AD-FICHIERS` et `SRV-APPEL`), SaaS métier `RésidGest` (sans MFA), accès de télémaintenance permanent par l'infogérant `InfoProx` via TeamViewer.

---

## 2. Atelier 1 : Cadrage et Socle de Sécurité
### Valeurs Métier (VM)
- **VM1 :** Dossiers résidents & suivi médico-social (SaaS `RésidGest`, postes de soins).
- **VM2 :** Dispositif d'alerte et d'appel d'urgence 24/7 (`SRV-APPEL`, médaillons, bornes DECT).
- **VM3 :** Facturation et administration / RH (`SRV-AD-FICHIERS`, partages SMB).
- **VM4 :** Sécurité physique et contrôle d'accès du bâtiment (caméras IP, badges).

### Événements Redoutés (ER) Majeurs
- **ER1 (VM2) :** Indisponibilité du système d'appel d'urgence > 2h -> **Gravité G4 (Critique)**.
- **ER2 (VM1) :** Divulgation ou exfiltration des dossiers de santé -> **Gravité G3 (Grave)**.
- **ER3 (VM3) :** Chiffrement par rançongiciel du serveur de fichiers -> **Gravité G3 (Grave)**.

---

## 3. Atelier 2 : Sources de Risques et Objectifs Visés
- **SR1 / OV1 :** Cybercriminels organisés (Ransomware / Double extorsion) -> *Retenu (Élevée)*.
- **SR2 / OV2 :** Escrocs opportunistes (Fraude au président / compromission M365) -> *Retenu (Moyenne)*.
- **SR3 / OV3 :** Visiteur ou tiers malveillant (intrusion depuis le Wi-Fi invités) -> *Retenu (Moyenne)*.

---

## 4. Atelier 3 : Écosystème et Scénarios Stratégiques
### Parties Prenantes (PP) Critiques
- **PP1 (InfoProx - Infogérant) :** Criticité Critique (accès TeamViewer permanent avec droits Admin Domaine).
- **PP3 (DomoSecur - Mainteneur IoT) :** Criticité Critique (mots de passe constructeur par défaut sur l'appel malade).

### Scénarios Stratégiques
- **SS1 :** Compromission par rebond via le prestataire informatique et déploiement d'un rançongiciel (G4).
- **SS2 :** Hameçonnage M365 sans MFA et exfiltration des dossiers de santé sur le SaaS `RésidGest` (G3).
- **SS3 :** Intrusion locale et sabotage de l'appel malade depuis le Wi-Fi invités non segmenté (G4).

---

## 5. Atelier 4 & 5 : Scénarios Opérationnels et Traitement (PACS)
- **SO1 :** Attaque MITRE ATT&CK (Accès distant `T1133` -> Scan réseau `T1046` -> Chiffrement `T1486`). Vraisemblance **V4 (Très élevée)**.
- **Plan d'Amélioration Continue de la Sécurité (PACS) :**
  - **M1 :** Segmentation du réseau en 4 VLANs (Admin, Postes, IoT/Sûreté, Wi-Fi Invités).
  - **M2 :** Suppression de TeamViewer et mise en place d'un accès VPN nominatif avec MFA pour les prestataires.
  - **M3 :** Activation du MFA sur M365/SaaS et durcissement Active Directory par GPO (ANSSI).
  - **M4 :** Sauvegardes 3-2-1 immuables hors domaine.
  - **M5 :** Déploiement d'un mini SIEM Wazuh pour la supervision temps réel.
