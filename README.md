# Prototype-synonym-generator
Ecrire une phrase sur interface Tkinter et obtenir nouvelles phrases en anglais et français 

# I-	Etapes conception informatique

Pour chercher des synonymes d’un mot anglais, j’utilise la bibliothèque nltk, et pour un mot français, PyMultiDictionary.
Remarque : on aurait pu utiliser cette dernière pour les deux langues mais j’avais déjà commencé le projet avec nltk.

a)	Traduction de la phrase + séparation des termes

Pour traduire la recherche faite en français ou en anglais, j’utilise la bibliothèque deep_translator.
Une fois traduite, la phrase est transformée en liste grâce à la fonction split() permettant de séparer tous les mots.

b)	Filtre des mots les plus pertinents

Grace à liste de mots obtenue, on cherche à savoir ceux dont on souhaite avoir un synonyme ou non. 

Nltk :

On utilise la fonction nltk.pos_tag() pour obtenir la nature du mot du mot anglais. On peut alors filtrer en supprimant déterminants, articles…( « TO », « DT », « IN »...)  

PyMultiDictionary :

On utilise la fonction dictionary.meaning() qui retourne une liste contenant la nature du mot et sa définition, pour un mot français. On filtre alors de la même manière.

Problème rencontré :
-	Le filtre ne fonctionne pas correctement sur certains mots français ayant plusieurs sens. Exemple : « ton » est à la fois un nom commun à conserver et un déterminant possessif à éliminer.

c)	Recherche des synonymes + conservation des N premiers

Nltk :

On cherche les synonymes des mots conservés avec la fonction wordnet.synsets().
On peut ensuite, grâce à la méthode de slicing, ne conserver que les N premiers synonymes fournis par la bibliothèque.

PyMultiDictionary :

On cherche les synonymes grâce à la fonction dictionary.synonym(). On réduit également le nombre de synonymes conservés.

Problèmes rencontrés :
-	Certains mots n’ont pas de synonymes trouvés, notamment les déterminants ayant échappé au filtre. Il faut donc supprimer parmi la liste de synonymes, les sous-listes vides [] avant de continuer. 
-	En sélectionnant les N premiers éléments, nous n’obtenons pas toujours les synonymes les plus pertinents…

d)	Association des synonymes + reconstruction phrases logiques

Après avoir obtenu une liste de tous les synonymes de la phrase de départ, on souhaite associer un synonyme de chaque mot ensemble. L’association est aléatoire avec la bibliothèque random. Une fois fait, on utilise la fonction replace() pour remplacer les mots de la phrase par leur synonyme associé. 

Problèmes rencontrés :
-	Reconstruire une phrase de cette manière fonctionne mal en français car l’accord en genre et en nombre n’est pas respecté.
-	Avec PyMultiDictionary, les verbes conjugués sont considérés parfois comme des noms communs (exemple : « est ») et doivent souvent être mis à l’infinitif.

e)	Augmenter le nombre de propositions et de synonymes

On créé deux fonctions permettant de modifier le nombre d’associations entre synonymes de manière aléatoire et donc de phrases construites, ainsi que de modifier le nombre N de synonymes conservés.

f)	Création de l’interface Tkinter


Grace à Tkinter, on créé une interface de cherche et d’affichage des différentes phrases construites en anglais et française, ainsi que la possibilité d’augmenter le nombre de propositions et de synonymes.

Problème rencontré :
-	Pour faire plusieurs recherches d’affilé, les anciennes phrases ne s’effacent par correctement et les nouvelles se mélangent avec.

# II-	rendu final 

 ![SharedScreenshot](https://user-images.githubusercontent.com/92324336/180181661-009ed81d-92d2-4884-a433-7c5b762397c6.jpg)

![SharedScreenshot2](https://user-images.githubusercontent.com/92324336/180181657-15069129-b62a-42cf-a53e-e979547b8c6e.jpg)

