# TP-02a-Gestion-des-abonnements-RBAC-Azure
La gestion des abonnements et le contrôle d'accès basé sur les rôles (RBAC) sont des mécanismes clés pour sécuriser et simplifier la gestion des droits d'accès dans les organisations. 

__Objectif du laboratoire__

<u>Dans ce laboratoire, vous allez apprendre à</u>:

Organiser vos abonnements Azure via des Groupes d’administration

Attribuer des rôles intégrés RBAC

Créer un rôle RBAC personnalisé

Surveiller les attributions via le Journal d’activité

Comprendre le format JSON des rôles RBAC

Manipuler les abonnements avec PowerShell et CLI

__🧩 TÂCHE 1 — Mettre en place les Groupes de gestion__
__Étapes :__

Connectez-vous au portail Azure

Ouvrez Microsoft Entra ID → Propriétés

Vérifiez : Gestion des accès aux ressources Azure

Recherchez Groupes de gestion

Cliquez sur + Créer

Saisissez :

ID : Polo-mg1

Nom : Polo-mg1

Soumettre

Actualiser la page

_À noter_

Le Root Management Group est créé par défaut

Tous les abonnements héritent de ses policies et RBAC

📸 Capture recommandée :

Vue des Management Groups

Propriétés → Gestion des accès aux ressources Azure

__🧩 TÂCHE 2 — Attribuer un rôle Azure intégré__
Objectif :

Donner au groupe Service Desk la capacité de gérer les machines virtuelles.

_Étapes :_

Sélectionnez le groupe d’administration : Polo-mg1

Ouvrez Contrôle d’accès (IAM) → Rôles

Parcourez les rôles intégrés

Cliquez sur + Ajouter → Ajouter une attribution de rôle

Choisissez : Contributeur de machine virtuelle

Membres → Ajouter le groupe helpdesk

Vérifier + attribuer (deux fois)

Vérifier que l’attribution est visible dans l’onglet Attributions

📸 Capture recommandée :

Vue du rôle sélectionné

IAM → Role Assignments

__🧩 TÂCHE 3 — Créer un rôle RBAC personnalisé__
_Objectif :_

Créer un rôle support permettant :

De créer des tickets

De gérer les demandes support
❗ Sans accès à l’enregistrement des fournisseurs Azure Support

Étapes :

Management Group → IAM

+ Ajouter → Ajouter un rôle personnalisé

Onglet Général :

Nom : Custom Support Request

Description :Un rôle de contributeur personnalisé pour les demandes d'assistance

Base permissions : Cloner un rôle

Choisir : Contributeur aux demandes d’assistance

Onglet Permissions

Cliquez Exclure des autorisations

Recherchez Microsoft.Support

Exclure : Other: Support resource provider registers

Onglet Étendues assignables :

Ajouter : /providers/Microsoft.Management/managementGroups/Polo-mg1

Vérifier + Créer

📸 Capture recommandée :

Rôle cloné

Permissions modifiées

JSON final

🧩 TÂCHE 4 — Surveiller les attributions via le Journal d’activité
Étapes :

Ouvrir le Management Group Polo-mg1

Journal d’activité

Filtrer par :

Operation : Create role assignment, Create custom role

Vérifier les événements

📸 Capture recommandée :

Journal filtré



Portail
Supprimer → Saisir le nom → Supprimer

PowerShell
Remove-AzResourceGroup -Name <resourceGroupName>

CLI
az group delete --name <resourceGroupName>

📊 Tableaux : Commandes importantes PowerShell et CLI Azure
__🔹 Tableau PowerShell – Abonnements
Commande__
Explication
Get-AzSubscription	Liste tous les abonnements accessibles
Set-AzContext -Subscription <ID>	Bascule sur un abonnement spécifique
Get-AzTenant	Affiche les informations du tenant
Get-AzRoleDefinition	Liste des rôles RBAC disponibles
Get-AzRoleAssignment	Montre les attributions de rôles actuelles
New-AzRoleDefinition -InputFile file.json	Crée un rôle RBAC personnalisé via JSON
New-AzManagementGroup -GroupName "Polo-mg1"	Crée un Management Group
Get-AzManagementGroup	Liste des Management Groups
__🔹 Tableau CLI – Abonnements
Commande__
Explication
az account list	Liste les abonnements
az account set --subscription <ID>	Change l’abonnement actif
az role definition list	Affiche la liste des rôles RBAC
az role assignment list	Liste les attributions de rôles
az role definition create --role-definition file.json	Crée un rôle personnalisé
az account show	Affiche l’abonnement actif
az managementgroup show --name Polo-mg1	Affiche un Management Group
az managementgroup list	Liste des Management Groups
📦 Quel est le format JSON Azure RBAC ?

Voici la structure :

{
  "Name": "Custom Support Request",
  "Id": null,
  "IsCustom": true,
  "Description": "A custom contributor role for support requests.",
  "Actions": [
    "Microsoft.Support/*"
  ],
  "NotActions": [
    "Microsoft.Support/register/action"
  ],
  "AssignableScopes": [
    "/providers/Microsoft.Management/managementGroups/az104-mg1"
  ]
}

__Éléments importants :__

Actions : opérations autorisées

NotActions : opérations explicitement interdites

AssignableScopes : où le rôle peut être attribué

__🛠️ Étapes pour créer un rôle RBAC personnalisé__

Identifier un rôle existant à cloner

Ouvrir IAM → Ajouter → Rôle personnalisé

Renseigner le nom et la description

Choisir un rôle à cloner

Modifier les permissions (Actions / NotActions)

Définir les étendues assignables

Vérifier

Créer le rôle

L’attribuer via IAM


__🏁 Points clés à retenir__

Les Management Groups structurent les abonnements

Les rôles RBAC permettent un contrôle granulaire

Les rôles peuvent être intégrés ou personnalisés

Les rôles sont définis dans un fichier JSON

Le Journal d’activité permet d’auditer les attributions
