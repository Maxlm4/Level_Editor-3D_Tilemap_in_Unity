# Level_Editor-3D_Tilemap_in_Unity

Ce projet Unity est un travail en cours, dont le code restera confidentiel, pour le moment du moins. Il s'agit d'un outil que je développe sur Unity grâce à Unity Editor, permettant de générer automatiquement un niveau en 3D en ne prenant seulement en entrée qu'une height map (potentiellement plusieurs). L'idée est simplement de gagner un maximum de temps sur la conception des environnements de mes prochains jeux en HD-2D, en ayant qu'à dessiner le terrain en pixelart et potentiellement remplacer les textures. De plus, tous les scripts, shaders et prefabs créés pour ce projet ont pour objectif d'être optimisés en temps d'exécution comme en espace mémoire et de stockage, et d'offrir un maximum de liberté sur la personnalisation de leurs paramètres.

This Unity project is a work in progress, which code files are still confidential for now. It is a tool I develop with Unity Editor. It allows fast and automatic generation of a whole 3D level only with a height map (maybe several) in input. It gives me time saving on my future HD-2D games environments design, by only asking me to draw some pixelart to generate the terrain and replace textures. Moreover, all scripts, shaders and prefabs created for this project are designed to achieve low execution time, low memory allocation and low project size on disk. They need to offer a great customization of their parameters.

============
Last version
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
