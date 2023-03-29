
# MAPD
Nous avons intégrer ce code dans le pneEditor dans le dossier PetriNet. Pour cela nous avons suivi le pattern adapter:
1- le target est le code préexistant du pneEditor dans les packages editor, save, util, workflow
2- l'adaptee est notre modèle de pétrinet. Il est dans le dossier petrinet du pneEditor et dans le package models. Il contient trois packages:Exceptions, filrouge, tests.Le package filrouge contient sept classes (classes PetriNet, Transition, Place, ArcIn, ArcOut et  ArcZero - ArcEmpty héritants de ArcIn ) et une interface qui permet d’implémenter notre réseau PetriNet.
3- l'adapter est le code qui nous permet de relier notre modèle de petrinet au target. Il est dans le dossier Petrinet et dans le package adapters.OUHAMMOU_KADDAMI. Il contient 4 classes: PetriNetAdapter, TransitionAdapter, ArcAdapter, PlaceAdapter.
## Le fonctionnement du code de notre modèle petrinet:
### Tirer une transition :
Pour tirer une transition, l’utilisateur appelle la méthode fire(Transition) de la classe PetriNet. Ensuite, La transition utilise la méthode IsFirable() pour s’assurer qu’elle est tirable. Pour cela,  les méthodes IsFirable() de tous ses arcs entrants sont appelés pour vérifier qu’ils sont activables.il appelle la fonction IsEnough(weight_arc) de la place qui lui est liée. La place donne une réponse à l’arc et celui-ci la transmet à la transition.

Ensuite, si la transition peut être tirée, il ne faut tirer que les arcs activables : la fonction fire() de la transition appelle alors la fonction isEnable() des arcs pour vérifier cette condition. Si l’arc est un arc normal il appelle la fonction IsEnough(int) de la place qui lui est liée avec comme argument le poids de l’arc. Si l’arc est un arc zéro il appelle la fonction IsEmpty() de la place, et si c’est un arc videur il appelle la fonction NotEmpty().  La place donne une 
réponse à l’arc qui est transmise à la transition. La transition appelle la méthode Enable() de tous les arcs activables  pour faire les changements nécessaires sur le 
réseau. Si l’arc est un arc videur la méthode de la appelée est empty(), sinon la méthode qui sera appelée est set_token(int) avec comme argument le poids de l’arc. 
### Construire un réseau de Petri:
L’utilisateur peut également construire ou modifier un réseau de Petri en utilsant les méthodes:add_place, add_transition,add_arcIn,add_arcOut,add_arcEmpty,add_Zero,remove_place,remove_transition,remove_arcIn,remove_arcOut, remove_arcEmpty, remove_Zero. Il peut aussi changer le poids d’un arc via les méthodes change_weight_ArcIn et change_weight_ArcOut, ou changer le nombre token d’une place en utilsant add_token et remove_token.
### Afficher le contenu d’un réseau de petri:
L’utilisateur peut visualiser le contenu d’un réseau en utilisant la méthode toStirng qui permet d’afficher le nombre de place,transition,arcIn et arcOut dans le réseau de Petri, ainsi que le nombre de jetons de chaque place , le poids et la nature des arcs. Nous avons utilisé toString  pour faire des tests plusieurs méthodes notamment tirer transition
### Les tests:
Nous avons fait 43 tests de toutes les méthodes de IPetriNet , les tests faites couvrent 100 % de notre code, et 99,2% du code test (les méthodes qui renvoient des exceptions ne sont pas couvertes dans le code test puisqu'elle ne doivent pas fonctionner et renvoyer une erreur ).

## Le fonctionnement du code de notre modèle petrinet:
1- ArcAdapter est l'adaptateur de AbstractArc
2- TransitionAdapter est l'adaptateur de AbstractTransition
3- PlaceAdapter est l'adaptateur de AbstractPlace
4- PetriNetAdapter est l'adaptateur de AbstactPetrinet

## Comment lancer le code de notre modèle PetriNet?:
### Construire un réseau de Pétri:
L'utilisateur instancie un objet de la classe IPetriNet avec le constructeur de la classe.
L'utilisateur doit d'abord créer les transitions et les places en utilisant les méthodes add_place et add_transition de PétriNet. Ces objets sont alors insérés dans les listes places et transitions du Petrinet selon leur ordre de création. 
Pour ajouter les arcs, l'utilisateur doit renseigner pour chacun la transition et la place qu'il relie, et si c'est arc entrant ArcIn /ArcZero/ArcEmpty dans la transition ou sortant de la transition ArcOut. Pour cela il faut utiliser la méthode qui convient parmi les méthodes suivantes: add_arcIn,add_arcOut,add_arcEmpty,add_Zero. Les objets sont alors insérés dans l'une des liste List_ArcsIn ou List_ArcsOut suivant l'ordre de création et selon le type.
L'utilisateur peut egalement retirer tout objet. S'il retire une place ou une transition les arcs liés sont retirés. 
### Tirer une transition :
Pour tirer une transition, l’utilisateur appelle la méthode fire(Transition) de la classe PetriNet.
### Utiliser le test:
Chaqu'un des 43 tests est commenté. L'utilisateur doit cliquer sur [Coverage AS --> JUnitTest] et vérifier qu'il n'y a pas d'erreur: Il ya des assertequals qui comparent les résultats attendus des méthodes avec le résultat obtenu. 

## Comment lancer le PNEEditor?:
Pour lancer le PNEEditor il suffit d'excuter la fonction main, puis on change le modèle, on choisissant le modèle intitulé OUHAMMOU_KADDAMI. Après on construit notre réseau PetriNet par l'ajout des places,transitions,arcs... on pourra aussi modfier ou ajouter le nombre de jetons d'une place et le poids de l'arc. Une fois le réseau PetriNet est construit, l'utilisatuer pourra tirer les transitions présentes dans le réseau.

##  Le lien entre le code et les modèles de conception:
Notre code est conforme aux modèles de conception(diagramme de classe et diagramme de séquence) que nous avons fait avant , la seule différence qui existe c’est que nous avons  ajouté les deux méthodes add_token et remove_token  dans la classe place,permettant de modifier le nb_token d’une place.
