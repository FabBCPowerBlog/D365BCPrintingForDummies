# D365BCPrintingForDummies

# Print with D365 Business Central for Dummies 

 

## Généralités

Depuis **Business Central**, il existe deux types d'impression :

- les impressions **interactives** : l'utilisateur demande l'édition d'un état, sélectionne l'imprimante à utiliser à travers le navigateur, puis lance l'impression en validant.
- les impressions **non-interactives** : une impression est lancée de manière automatisée, l'intervention de l'utilisateur n'est pas demandée (Exemples : impression automatique de documents ou d'étiquettes quand on manipule un Device). Il se pose alors la question de la sélection de l'imprimante à utiliser.

## En SaaS

### Généralités

Quand **Business Central** est hébergé en SaaS, les impressions interactives sont possibles car l'impression est prise en charge par le navigateur internet : l'utilisateur va notamment pouvoir sélectionner l'imprimante à utiliser et l'impression va pouvoir être envoyée vers les imprimantes installées et connectées au poste client.

Par contre, les impressions non-interactives nécessitent une attention particulière. En effet, dans le contexte SaaS, le serveur **Business Central** ne peut en aucun cas communiquer directement avec les ressources locales chez le client, ce qui inclu les imprimantes. Pour ce type d'impression, il est donc nécessaire d'utiliser un service web de gestion des imprimantes. Le principe de ce service web va être le suivant :

- Une souscription est réalisée auprès d'un service web d'impression (exemple : Print Node)
- Une application est installée dans l'environnement local du client : cette application servira de passerelle entre le service web et les imprimantes locales chez le client.
- A la demande d'impression, **Business Central** transmets les informations nécessaires au service web (contenu à imprimer, imprimante à utiliser...) et le service web déclenche l'impression sur l'imprimante locale via la passerelle    

A noter que, pour les impressions interactives, si on souhaite qu'une imprimante particulière soit automatiquement proposée pour un utilisateur et une édition, il est nécessaire de passer par un service web d'impression. En effet, cet automatisme nécessite un paramétrage au niveau de **Business Central**, et ce paramétrage ne peut pas être réalisé avec les imprimantes locales.

### Print Node

https://www.printnode.com/fr

Le service **Print Node** est un service web d'impression.

#### Fonctionnement

Le service **Print Node** peut être utilisé de deux façons :

- **Via email** : chaque imprimante recensée via la plateforme **Print Node** hérite d'une adresse email. Si un email est envoyé à l'une de ces adresses avec un document en pièce jointe, le document est alors automatiquement imprimé.
- **Via webservice** : le service **Print Node** expose un ensemble d'API qui peuvent être invoquées depuis **Business Central** afin de lancer les impressions. 

Dans les deux cas d'utilisation, il est nécessaire d'installer un client local qui servira de passerelle entre le service web et les ressources locales.
https://www.printnode.com/fr/docs/installation/windows

La console d'administration de printnode (https://api.printnode.com/app/devices) permet de  :
- Consulter les imprimantes disponibles sur le compte print node.
- Consulter les adresses e-mail de chaque imprimante.
- Définir une whitelist des e-mail autorisés à utiliser le service.
- Tester l'impression sur les imprimantes.

#### Tarif

https://www.printnode.com/fr/pricing

#### Utilisation via email avec Business Central

Depuis **Business Central**, il est possible d'utiliser le service **Print Node** via email sans installer d'app tierce. Il suffit de définir des **imprimantes par e-mail** depuis la page **Gestion de l'impression**. Chaque impression donnera lieu à l'envoi d'un email avec le document à imprimer en pièce jointe et donc lancera l'impression sur l'imprimante.

**Attention !** Ce fonctionnement nécessite de paramétrer un compte de messagerie afin que **Business Central** puisse émettre les emails vers le service web.

Pour paramétrer des imprimantes par mail 
https://learn.microsoft.com/fr-fr/dynamics365/business-central/admin-printer-setup-email

#### Utilisation via webservice avec Business Central

Pour utiliser **Print Node** via webservice, le plus simple est d'utiliser un connecteur disponible depuis l'AppSource.

- **Insight Works PrintNode Connector**
https://appsource.microsoft.com/en-us/product/dynamics-365-business-central/PUBID.insight-works%7CAID.b0c8bcc7-2924-4cd2-8562-4e71ebd07323%7CPAPPID.b0c8bcc7-2924-4cd2-8562-4e71ebd07323?tab=Overview
  
- **VLC PrintNode Integration**
https://appsource.microsoft.com/en-us/product/dynamics-365-business-central/PUBID.vlc-solutions-llc-1263055%7CAID.vlc_printnode_integration%7CPAPPID.fb6dcfa1-3e74-4afc-a197-58b72ddf118a?tab=Overview
