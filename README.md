# angulargetstarted

## Créer la liste des produits
Dans cette section nous mettrons à jour l'application afin qu'elle affiche une liste de produits.
Nous utiliserons des données prédefinies  depuis products.ts
ainsi que des fichiers et méthode depuis product-list.component.ts.  Cette section nous guide afin d'éditer l'HTML aussi connu sous le nom de modèle.

#1
On construit des applications Angular avec des composants qui définissent des zones de responsabilité dans l'interface utilisateur qui permettent de réutiliser des fonctionnalités d'interface utilisateur
Un composant est composé de 3 choses :
    1. une classe de composant qui peut gérer données et        fonctionnalités
    2. un modèle html qui détermine l'interface graphique
    3. des styles spécifiques au composant qui définissent la   vue et le design

#2 Avec *ngFor est une directive structuerelle qui donne un rendu pour chaque item d'une collection.
la div se répète pour chaque produit dans la liste afin de l'afficher dans l'élément div.

Cette directive structurelle remodèle la structure du  DOM  en ajoutant, enlevant et en manipulant les éléments.

#3
Interpolation {{ }} nous permet de renvoyer la valeur de la propriété en tant que texte. chaque nom produit est pointé dynamiquement par {{ product.name }}

#4
utiliser une directive : *ngIf afin qu'Angular crée seulement un élément p si le produit courant a une desription.

L'application affiche maintenant le nom et la description de chaque produit dans la liste. Si la description est vide la condition if fonctionne et empêche la création d'un élément <p>

#5 nous ajoutons un bouton qui détecte les événement clik



## Passer des données à un composant enfant
la liste des produits affiche le nom et la description de chaque produit.
Le composant ProductListComponent définit une propriété des produits qui contient des données importées pour chaque produit depuis le tableau products dans products.ts
 
la prochaine étape est de créer une nouvellle fonctionnalité "alerte" qui utilise les données des produits depuis le composant ProductListComponent. L'alerte vérifie le prix du produit et si le produit est plus cher que 700$ alors elle affiche un bouton de notification qui permet à l'utilisateur de de s'inscrire pour recevoir une notification quand le produit est en soldes.

Cette section parcourt les étapes pour créer un composant enfant ProductAlertsComponent, qui peut recevoir des données depuis le composant parent ProductListComponent

#1 On génère un composant product-alerts à l'aide de la commande suivante
ng generate component product-alerts

#2 les principales fonctionnalités du décorateur @Component
sont les suivantes :


The @Component() definition also exports the class, , which handles functionality for the component.
1. le selecteur app-product-alerts identifie le composant. 
2. modèle et style url
3. la class d'exportations ProductAlertsComponentqui gère la fonctionnalité pour le component.

#3  Dans la définiton de classe ProductAlertsComponent, définie une propriété nommée avec un @Input decorateur. Celle ci indique que la valeur de la propriété est passée depuis le composant parent.
The @Input() decorator indicates that the property value passes in from the component's parent, ProductListComponent.

#4 Pour configurer ProductAlertsComponent à recevoir les données de produit, il faut d'abord importer Input depuis @angular/core

#5 Dans la définition de classe ProductAlertComponent, définissez une propriété nommée product avec un @Input décorateur. @Input indique que la valeur de la propriété est transmise depuis le composant parent ProductListComponent

#6 Le générateur a automatiquement ajouté ProductAlertsComponent à AppModule pour le rendre disponible aux autres composants de l'application

#7 Finalement, pour afficher ProductAlertsComponent en tant qu'enfant de ProductListComponent, ajoutez le <app-product-alerts> élement àproduct-list.component.html. Ensuite, passez le produit courant en tant qu'input vers le composant utilisant la propriété afférante.

#8 Le nouveau composant product alert prend un produit en input depuis la list produit. Avec cet input il montre ou cach le bouton Notify Me basé sur le prix du produit. Le Phone XL est plus cher que 700$ donc le bouton notify me apparait sur ce produit.

### Transmettre des données vers un composant parent

Pour faire fonctionner le bouton Notify Me, le composant enfant a besoin de notifier et passer les données au composant parent.

Le composant ProductAlertsComponent a besoin d'emettre un événement quand l'utilisateur clique sur le bouton Notify Meet le ProductListComponent a besoin de répondre à l'événement.

Dans un nouveau composant, Le Générateur Angular inclut un constructor vide, l'interface Oninit et la méthode ngOnInit().
A partir de ces étapes ne les utilisez pas, les exemples de code suivant les omettent pour rendre le code plus bref.

#1 import de output et EventEmitter depuis @angular/core

#2 Dans la classe du composant définissez une propriété nommée notify avec un @Output decorateur et une instance de EventEmitter() en configurant ProductAlertsComponent avec un @output qui permet ProductAlertsComponent d'émettre un événement quand la valeur de la propriété notify change.

#3 dans product-alerts.component.html mettez à jour le bouton Notify Me avec un lien d'événement pour appeler la méthode notify.emit()

#4 Définissez le comportement qui arrive quand l'utilisateur clique sur le bouton. Le parent, ProductListComponent -et non le composant ProductAlertsComponent- agit quand l'enfant active l'événement. Dans pro product-list.component.ts définissez une méthode onNotify() similaire à la méthode share().

#5 Mettez à jour le composant ProductListComponent pour recevoir des données depuis ProductAlertsComponent.
Dans product-list.component.html liez <app-product-alerts> à la méthode onNotify() du composant liste produit. <app-product-alerts> est ce qui affiche le bouton Notify Me.

### ajouter la navigation

Nous allons ajouter des fonctionnalités à l'application :
1. taper une URL dans la barre d'adresse pour naviguer vers la page produit correspondante
2. cliquer des liens pour naviguer à l'intérieur de notre application single-page
3. Cliquer les les boutons suivant et retour du navigateur pour naviguer dans l'historique intuitivement

## Associer un chemin URL avec un composant

L'app uttilise déjà le Router Angular pour naviguer vers le composant ProductListComponent. Cette section montre comment définir une route pour montrer les détails individuel d'un produit

#1 Générer un nouveau composant pour les détails produit.
Dans le terminal avec ng generate component product-details.

#2 Dans app.module.ts ajoutez une route pour les détails produit avec path de products/:productId et 
ProductDetailsComponent pour le composant

#3 Ouvrir le product-list.component.html

#4 Modifier le nom de l'ancre du produit pour inclure un routerLink avec le product.id en tant que paramètre
la directive routerLink nous aide à personnaliser l'ancre. Dans ce cas la route ou URL contient un segment fixe /products. Le segment final est variable en insérant la propriété id du produit courant.
Par exempl, l'URL pour un produit avec l'id 1 devrait ressembler à https://getting-started-myfork.stackblitz.io/products/1

#5 vérifier que le router fonctionne comme prévu en cliquant le nom du produit. L'application devrait afficher ProductDetailsComponent qui dit actuellement 
 "product-details works!"

Notez que l'URL dans la fenêtre de prévisualisation change le segment final est products/# où #est le nombre de la route sur laquelle on a cliqué.

## Voir les détails produits

Le composant ProductDetailsComponent gère l'affichage de chaque produit. Le routeur Angular affiche l'URL du navigateur bas& sur le composant et définit les routes.

Dans cette section vous utiliserez le routeur Angular pour combinenr les données produit et l'information de la route pour afficher les détails spécifique pour chaque produit.

#1 Dans product-details.component.ts importons ActivatedRoute depuis @angular/router, et le tableau des produits depuis ../products.

#2 Définissons la propriété de produit

#3 Injectons ActivatedRoute dans le constructor en ajoutant private route: ActivatedRoute en tant qu'argumant à l'intérieur des parenthèses du constructor

ActivatedRoute est spécifique à chaque composant que le routeur Angular charge. ActivatedRoute contient des informations à propos de la route et de ses paramètres.
En injectant ActivatedRoute nous configurons le composant pour utiliser un service. L'étape Gestion des Données couvre les services en détail.

#4 Dans la méthode ngOnInit() extrayons le productId depuis les paramètres de la route et trouvons le produit correspondant dans le tableau produit.

#5 Mettons à jour le gabartit ProductDetailsComponent pour afficher les détails produits avec un *ngIf. Si le prodit existe la div est rendue dynamiquement avec un nom, un prix et une description

La ligne h4 utilise un currency pipe pour transformer un nombre en une chaine de caractère de monnaie. Un tuyau est une façon de transformer des données dans notre gabarit HTML. 

Quand les utilisateurs cliquent sur le nom d'un produit de la liste, le routeur navigue vers l'URL distincter du produit, le routeur affiche les détails du produit.

### Gérer des données

 A ce stade Nous avons deux vues une liste produit et les détails produit.
 L'utilisateur peut cliquer sur le nom d'un produit pour voir les détails du produit dans une nouvelle vue, avec une URL ou route distincte.
 Cette étape du tutoriel nous guide pour créer un panier de courses avec les phases suivantes :
 1. Mettre à jour la vue des détails produits pour inclure un bouton Achat qui ajoute le produit actuel à une liste de produits que le service du panier gère.
 2. Ajouter un composant panier qui affiche les produits dans le panier
 3. ajouter un composant livraison qui récupère les prix de livraison pour les produits dans le panier en utilisant HttpClient pour récupérer des données depuis un fichier .json

## Créer un service de panier d'achat.

Dans Angular, un service est une instance d'une classe que l'on peut rendre disponible pour toute partie de l'application en utilisant le système d'injection de dépendance.

Actuellement, les utilisateurs peuvent voir les informations d'un produit et l'application peut simuler le partage et les notifications à propos des changements d'un produit.

La prochaine étape est de construire une façon pour les utilisateur d'ajouter un produit à leur panier.
Cette section explique comment ajouter un bouton acheter et installer un service de panier pour stocker des informations à propos des produits dans le panier.

