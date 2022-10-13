# Level_Editor-3D_Tilemap_in_Unity

Ce projet Unity est un travail en cours, dont le code restera confidentiel, pour le moment du moins. Il s'agit d'un outil que je développe sur Unity grâce à Unity Editor, permettant de générer automatiquement un niveau en 3D en ne prenant seulement en entrée qu'une height map (potentiellement plusieurs). L'idée est simplement de gagner un maximum de temps sur la conception des environnements de mes prochains jeux en HD-2D, en ayant qu'à dessiner le terrain en pixelart et potentiellement remplacer les textures. De plus, tous les scripts, shaders et prefabs créés pour ce projet ont pour objectif d'être optimisés en temps d'exécution comme en espace mémoire et de stockage, et d'offrir un maximum de liberté sur la personnalisation de leurs paramètres.

Un éditeur en temps réel serait approprié à ce genre d'usage, mais je sais d'expérience que cela me prendrait plus de temps de créer un niveau à la main dans Unity que de le dessiner en pixelart puis de le générer, quitte à retoucher le niveau ensuite à la main ou sur Blender.

This Unity project is a work in progress, which code files are still confidential for now. It is a tool I develop with Unity Editor. It allows fast and automatic generation of a whole 3D level only with a height map (maybe several) in input. It gives me time saving on my future HD-2D games environments design, by only asking me to draw some pixelart to generate the terrain and replace textures. Moreover, all scripts, shaders and prefabs created for this project are designed to achieve low execution time, low memory allocation and low project size on disk. They need to offer a great customization of their parameters.

A real time editor would be appropriate with this situation, but I know from experience I would spend too much time creating the level by hand in Unity. I prefer to draw it in pixelart and generate it, even if it means some afterwards polishing by hand or with Blender.

=====================
Latest : Version 0.2
=====================

La gestion de l'application de textures sur le terrain généré a été ajoutée. Seul un fichier .png (ou autre extension d'image) est nécessaire pour texturer tout le sol. Si des imperfections sont visibles, il s'agit de problèmes liés à ma texture et non au mappage UV, que j'ai pris soin d'effectuer correctement. Je me concentre pour le moment plus sur la partie développement du level editor que sur la qualité graphique du rendu. De plus on peut observer des variations sur la texture d'herbe (la présence de fleurs). Ces variations sont pour le moment aléatoires, mais seront plus tard implémentées afin d'être générées selon une image en entrée ou en utilisant un bruit (pour simuler les parterres de fleurs par exemple).

I added the texturing process to the project. A simple image file is needed to texture everything. If imperfections can be found, they are only due to my texture file, I took a good care of my UV maping. For now, I focus more on the level editor development than that visual aspect of my test level. Moreover, we can see flowers sometimes on the grass floor, because I added some randomness in the texture mapping. Later, I will add that kind of texture generation from an image file or depending on a noise map (for example to simulate flowerbeds).

<p align="center"><img src="https://user-images.githubusercontent.com/36695417/195469416-cadff72f-a73d-47d8-8b32-839c7a9759c7.png"></p>
<p align="center">the terrain with textures</p>

J'ai aussi apporté un soin particulier à l'optimisation en supprimant les faces inutiles des meshs et en fusionnant toutes mes tuiles en un seul mesh. Ainsi, j'ai pu économiser pas mal de ressources.

I took a good care of the optimization process, deleting every useless faces and merging the tiles in a single mesh. So that I can save a lot of fps.

<p align="center"><img src="https://user-images.githubusercontent.com/36695417/195469672-982b26e3-4a1d-41b0-8c8e-f0fc986bc26c.png"></p>
<p align="center">a downside view</p>

Pour ceux qui se demandent à quoi ressemble mon éditeur dans Unity, il s'agit simplement d'un bouton "build" sur le script principal. Bien d'autres scripts sont présents sur un objet "level", car je développe chaque script en tant que MonoBehaviour, tous n'ont qu'un seul rôle. Le script "Level Builder" a pour rôle de distribuer les données nécessaires aux autres scripts et de rassembler les résultats en sortie.

For those asking what my editor looks like in Unity, it is just a simple "build" button on my main script. A lot more scripts are associated with the "level" object, because they all are MonoBehaviours, so they only have one purpose. The "Level Builder" script goal is to share data needed by the other scripts and gather their output.

<p align="center"><img src="https://user-images.githubusercontent.com/36695417/195469802-d2120da6-f4b1-41dc-8865-db9af2e8ae42.png"></p>
<p align="center">a downside view</p>

Je sais qu'en utilisant juste les niveaux de gris sur mon image représentant le niveau je peux obtenir ce résultat sans avoir besoin d'un classificateur de couleurs, mais je préfère personnellement les couleurs pour une meilleure lisibilité lors du dessin.

I know I only need greyscale for the picture representing my level to get the same result without a color classificator, but I prefer drawing with colors, as I find it more readable.

============
Version 0.1
============

Actuellement, je dispose d'un script me permettant de générer un terrain (en bleu) dans un premier temps d'après une height map en entrée. Un second script ajoute par dessus des adoucissements (en rouge), pour que le terrain généré sois plus agréable à voir et ressemble moins à un jeu comme Minecraft.

For now, I developed a first script able to generate terrain (in blue) with a height map in input. A second script adds smoothness to the terrain (in red), making it a lot less like minecraft visually.


<p align="center"><img src="https://user-images.githubusercontent.com/36695417/194674299-89d5274d-5af5-469a-9b13-88547a53dd4c.png"></p>
<p align="center">the input height map</p>

<p align="center"><img src="https://user-images.githubusercontent.com/36695417/194674257-63976549-989d-43a5-9dd5-f0993cb4d9c0.png"></p>
<p align="center">the terrain generated</p>


Le projet est en HDRP afin d'accéder facilement aux différentes options graphiques qui rendent des jeux comme Octopath Traveler aussi beaux. J'ai ajouter une "sky and fog box" à l'éditeur de niveau afin de pouvoir éditer directement le brouillard une fois le niveau généré. J'ajouterai probablement un script plus tard pour améliorer la personnalisation des brouillards et des lumières.

The project is in HDRP for easy access to graphical options that makes a game like Octopath Traveler that beautiful. I added a "sky and fog box" to the editor to edit fog once the level generation is done. I will probably add a script to modify fog and lighting easily later.


<p align="center"><img src="https://user-images.githubusercontent.com/36695417/194674784-a8d66d43-c9ad-4778-9cde-97ac1c763162.png"></p>
<p align="center">HDRP fog and lighting added</p>


De plus, une autre map permet de placer des sprites sur le terrain après sa génération. Ces sprites sont animés pour simuler l'effet du vent et sont sensibles à la lumière de l'environnement grâce à un shader que j'ai conçu. Pour l'instant ces sprites sont des plantes, mais à l'avenir les plantes (le foliage) sera probablement géré autrement (procéduralement par exemple). Les sprites placés via map seront utiles pour placer plus rapidement des éléments du décor comme des tonneaux ou des lampadaires.

Moreover, another map allows sprite placement on the generated terrain. These sprites are animated to simulate wind effect and are subject to environment lightings, thanks to a shader I made. For now sprites are grass and flowers, but I think I will generate foliage in another way in the future (procedural generation maybe). Sprites placed from a map will be useful for decorations such as barrels or lampposts.


<p align="center"><img src="https://user-images.githubusercontent.com/36695417/194675398-b5d8069c-9a08-4590-aaef-4af7ff6f7d7e.gif"></p>
<p align="center">Animated sprites</p>
