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

