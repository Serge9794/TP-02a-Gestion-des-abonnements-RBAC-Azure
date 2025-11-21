# TP-02a-Gestion-des-abonnements-RBAC-Azure
La gestion des abonnements et le contrôle d'accès basé sur les rôles (RBAC) sont des mécanismes clés pour sécuriser et simplifier la gestion des droits d'accès dans les organisations. 

__Objectif du laboratoire__

Dans ce laboratoire, vous allez apprendre à:

-Organiser vos abonnements Azure via des Groupes d’administration,

-Attribuer des rôles intégrés RBAC,

-Créer un rôle RBAC personnalisé,

-Surveiller les attributions via le Journal d’activité,

-Comprendre le format JSON des rôles RBAC.


__🧩 TÂCHE 1 — Mettre en place les Groupes de gestion__

__Étapes :__


-Connectez-vous au portail Azure,

-Ouvrez Microsoft Entra ID → Propriétés,

-Vérifiez : Gestion des accès aux ressources Azure,

-Recherchez Groupes de gestion,

-Cliquez sur + Créer

Saisissez :

.ID : Polo-mg1

.Nom : Polo-mg1

.Soumettre

.Actualiser la page


_À noter_


Le Root Management Group est créé par défaut

Tous les abonnements héritent de ses policies et RBAC


__📸 Captures__




<img width="1167" height="744" alt="T11" src="https://github.com/user-attachments/assets/f4c4b37c-0c36-4184-b4f2-d6276829630f" />



<img width="1187" height="925" alt="T11 (3)" src="https://github.com/user-attachments/assets/a17360ee-fd02-44ee-b313-4b84a7eea699" />



<img width="1209" height="899" alt="T11 (2)" src="https://github.com/user-attachments/assets/f78bd6ac-abe1-462f-b070-935192db5218" />




__🧩 TÂCHE 2 — Attribuer un rôle Azure intégré__


__Objectif :__

Donner au groupe Service Desk la capacité de gérer les machines virtuelles.

__Étapes :__


*Sélectionnez le groupe d’administration : Polo-mg1,

*Ouvrez Contrôle d’accès (IAM) → Rôles,

*Parcourez les rôles intégrés,

*Cliquez sur + Ajouter → Ajouter une attribution de rôle,

*Choisissez : Contributeur de machine virtuelle,

*Membres → Ajouter le groupe helpdesk,

*Vérifier + attribuer (deux fois),

*Vérifier que l’attribution est visible dans l’onglet Attributions,


__📸 Captures :__



<img width="1211" height="917" alt="T24" src="https://github.com/user-attachments/assets/a4fac366-8847-4002-ac91-9ffa002e6008" />


<img width="1208" height="906" alt="T23" src="https://github.com/user-attachments/assets/989ad78c-c59e-4339-8ae4-17fe07db1eb7" />


<img width="1216" height="903" alt="T22 (2)" src="https://github.com/user-attachments/assets/9122dd70-d3c9-40c3-9c4e-aa984978ae2c" />


<img width="1201" height="884" alt="T21" src="https://github.com/user-attachments/assets/5439aad9-3738-462c-b1c0-92667f67fb2f" />


<img width="1212" height="919" alt="T25" src="https://github.com/user-attachments/assets/8ef61d1a-146a-4255-aa49-8e416726679c" />





__🧩 TÂCHE 3 — Créer un rôle RBAC personnalisé__


__Objectif :__


Créer un rôle support permettant :

-De créer des tickets support,

-De gérer les demandes support (Sans accès à l’enregistrement des fournisseurs Azure Support),

            __Etapes:__

*Management Group → IAM + Ajouter → Ajouter un rôle personnalisé

Onglet Général :

*Nom : Custom Support Request(role personnalisé)

*Description :Un rôle de contributeur personnalisé pour les demandes d'assistance

*Base permissions : Cloner un rôle

*Choisir : Contributeur aux demandes d’assistance

Onglet Permissions

*Cliquez Exclure des autorisations

*Recherchez Microsoft.Support

*Exclure : Other: Support resource provider registers

*Onglet Étendues assignables : Ajouter : /providers/Microsoft.Management/managementGroups/Polo-mg1

*Vérifier + Créer

  __📸 Captures:__

<img width="1240" height="884" alt="T33" src="https://github.com/user-attachments/assets/8ebb3b6d-33c8-4f9f-96b9-0bd13ef40ad5" />
<img width="1214" height="905" alt="T32" src="https://github.com/user-attachments/assets/a5932f00-0df8-490c-a4ab-e86e682a350c" />
<img width="1224" height="930" alt="T31" src="https://github.com/user-attachments/assets/7cf5c143-afd1-417c-a2aa-2dbaacc11eca" />
<img width="1246" height="854" alt="T37" src="https://github.com/user-attachments/assets/5e1ba8a5-146d-4ccb-95f2-76795a36447f" />
<img width="1207" height="858" alt="T36" src="https://github.com/user-attachments/assets/176e12f2-ea27-4f89-ac62-ecad214839e4" />
<img width="1205" height="869" alt="T35" src="https://github.com/user-attachments/assets/ee2a483b-1b85-411e-9661-a1deaa7bd19b" />
<img width="1182" height="903" alt="T34" src="https://github.com/user-attachments/assets/58b131c9-45f2-47e0-9f18-fdba0d83cd1b" />



__🧩 TÂCHE 4 — Surveiller les attributions via le Journal d’activité__

__Étapes :__

*Ouvrir le Management Group Polo-mg1,

*Journal d’activité,

*Filtrer par : Operation : Create role assignment, Create custom role,

*Vérifier les événements

  __📸 Capture du Journal filtré:__

<img width="1227" height="885" alt="T4" src="https://github.com/user-attachments/assets/a0cf244a-f6bd-493f-9f4c-8406b7c35d96" />






__Commandes importantes PowerShell et CLI Azure__

__🔹  PowerShell – Abonnements Commande__

      Explication
*Get-AzSubscription :	Liste tous les abonnements accessibles,

*Set-AzContext -Subscription <ID>	: Bascule sur un abonnement spécifique,

*Get-AzTenant	: Affiche les informations du tenant,

*Get-AzRoleDefinition:	Liste des rôles RBAC disponibles,

*Get-AzRoleAssignment:	Montre les attributions de rôles actuelles,

*New-AzRoleDefinition -InputFile file.json:	Crée un rôle RBAC personnalisé via JSON,

*New-AzManagementGroup -GroupName "Polo-mg1"	:Crée un Management Group,

*Get-AzManagementGroup	Liste des Management Groups.

__🔹 Tableau CLI – Abonnements Commande__

     Explication
*az account list:	Liste les abonnements,

*az account set --subscription <ID>:	Change l’abonnement actif,

*az role definition list:	Affiche la liste des rôles RBAC,

*az role assignment list:	Liste les attributions de rôles,

*az role definition create --role-definition file.json:	Crée un rôle personnalisé,

*az account show:	Affiche l’abonnement actif,

*az managementgroup show --name Polo-mg1 :	Affiche un Management Group,

*az managementgroup list :	Liste des Management Groups.


__Éléments importants :__

*Actions : opérations autorisées

*NotActions : opérations explicitement interdites

*AssignableScopes : où le rôle peut être attribué

__🛠️ Étapes pour créer un rôle RBAC personnalisé__

*Identifier un rôle existant à cloner

*Ouvrir IAM → Ajouter → Rôle personnalisé

*Renseigner le nom et la description

*Choisir un rôle à cloner

*Modifier les permissions (Actions / NotActions)

*Définir les étendues assignables

*Vérifier

*Créer le rôle

*L’attribuer via IAM


__🏁 Points clés à retenir__

-Les Management Groups structurent les abonnements

-Les rôles RBAC permettent un contrôle granulaire

-Les rôles peuvent être intégrés ou personnalisés

-Les rôles sont définis dans un fichier JSON

-Le Journal d’activité permet d’auditer les attributions
