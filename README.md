# Level_Editor-3D_Tilemap_in_Unity

Ce projet Unity est un travail en cours, dont le code restera confidentiel, pour le moment du moins. Il s'agit d'un outil que je développe sur Unity grâce à Unity Editor, permettant de générer automatiquement un niveau en 3D en ne prenant seulement en entrée qu'une height map (potentiellement plusieurs). L'idée est simplement de gagner un maximum de temps sur la conception des environnements de mes prochains jeux en HD-2D, en ayant qu'à dessiner le terrain en pixelart et potentiellement remplacer les textures. De plus, tous les scripts, shaders et prefabs créés pour ce projet ont pour objectif d'être optimisés en temps d'exécution comme en espace mémoire et de stockage, et d'offrir un maximum de liberté sur la personnalisation de leurs paramètres.

Un éditeur en temps réel serait approprié à ce genre d'usage, mais je sais d'expérience que cela me prendrait plus de temps de créer un niveau à la main dans Unity que de le dessiner en pixelart puis de le générer, quitte à retoucher le niveau ensuite à la main ou sur Blender.

This Unity project is a work in progress, which code files are still confidential for now. It is a tool I develop with Unity Editor. It allows fast and automatic generation of a whole 3D level only with a height map (maybe several) in input. It gives me time saving on my future HD-2D games environments design, by only asking me to draw some pixelart to generate the terrain and replace textures. Moreover, all scripts, shaders and prefabs created for this project are designed to achieve low execution time, low memory allocation and low project size on disk. They need to offer a great customization of their parameters.

A real time editor would be appropriate with this situation, but I know from experience I would spend too much time creating the level by hand in Unity. I prefer to draw it in pixelart and generate it, even if it means some afterwards polishing by hand or with Blender.

=====================
Latest : Version 0.4
=====================

Premier changement important de cette version, la ligne de rendue a été modifiée pour l'URP. En effet, étant donné la quantité colossale de post-processing requise pour créer des jeux HD-2D les plus beaux, HDRP s'est rapidement avéré être une mauvaise solution, car trop réaliste et donc pas assez stylisé, trop coûteux en performances, et trop peu personnalisable. Pour un même rendu, j'ai obtenu 180 fps sur URP contre 80 fps sur HDRP. De plus, la documentation sur URP semble être plus fournie que celle d'HDRP.
La carte a été agrandie pour tester les performances du générateur sur des cartes de tailles envisageables dans un jeu. Ainsi, pour une carte de taille 50x5x100 blocs, le générateur met moins de 3 secondes pour créer le mesh et y appliquer les bonnes textures, ce qui est un temps plus que raisonnable comparé à d'autres générateurs que j'ai pu tester mettant environ 1 minutes pour générer une carte de taille similaire. Un mesh en forme de cuve a été rajouté sur la carte pour éviter les problèmes de fuites lumineuses.

Important note before getting into the version news, the render pipeline has been changed for URP. The best HD-2D games require a lot of post-processing to look good, so I needed a render pipeline light in performance costs, easy to customize and no so realistic (stylised game art is often better in these cases). For the same render, I got 180 fps with URP, but only 80 fps with HDRP. Moreover, the URP documentation seems a little better.
The map is now larger, because I needed to test the generator performances for the generation of a map with a real case size. For a 50x5x100 blocs map, the generator took 3 seconds, which is not so bad compared to the 60 seconds other generators I tested needed to generate a similar map. I added a cuve shaped mesh to avoid light bleeding on the terrain.

<p align="center"><img src="https://user-images.githubusercontent.com/36695417/200186185-4a05378c-4a44-4c83-b701-888b026ff531.png"></p>
<p align="center">the new generated terrain</p>

J'ai ensuite implémenté mon shader d'eau, et un script permettant de fusionner toutes les surfaces du même type d'eau pour accroître encore les performances. Seule la réflection planaire a été désactivée, car trop coûteuse en performances, non nécessaire pour avoir un visuel satisfaisant et impossible à implémenter tel quelle pour plusieurs surfaces d'eau. J'ai également testé l'ajout des mipmaps pour éviter les clignotements des textures au loin. Ils fonctionnent à merveille, sauf que mon atlas de texture actuel n'est pas d'une résolution suffisamment bonne pour obtenir un effet visuel acceptable. De plus, mon atlas possèdes toutes ses textures collées les unes aux autres, ce qui provoque des problèmes de normales sur les bords des faces de mon terrain. Cependant, la mise à jour de mon atlas ne faisant pas partie intégrante de l'éditeur de niveau, celle-ci est remise à plus tard. Pour le moment, les mipmaps ne seront pas utilisées dans cette vitrine pour ces raisons.

Then, I added my personal water shader and a script to merge the water surfaces of the same type together to increase once more performances. I only disabled the planar reflection, because of its performance cost, its unnecesary visual addition, and the fact I can't do planar reflection for several water planes in the current shader state. I added mipmaps too to avoid texture flickering. They work wonderfully, but my texture atlas is not big enought to make it that beautiful, and the sub textures inside it are all stick next each other, so I can sometime see normal leaking on the mesh edges. But I'm not focusing on getting the best visual quality for now, so I will modify my texture atlas only in a while. For these reasons, I will not use mipmap in this showcase for a moment.

<p align="center"><img src="https://user-images.githubusercontent.com/36695417/200186830-e66991bb-4edc-439c-8b25-0a2442c61d1a.png"></p>
<p align="center">water surfaces and mipmaps</p>

Ensuite, j'ai créé un shader de skybox procédurale soumis à un cycle jour/nut, permettant de contrôler la couleurs de la skybox, de la lumière, des astres lumineux et l'apparition d'étoiles au fil du temps et de la luminosité ambiante. J'ai ajouté à cela une probe customisée pour refléter correctement la lumière sur la scène quasiment sans impact sur les performances. Les paramètres liés à la lumière, aux textures et aux reflections sont stockées dans un fichier au lieu du material directement pour permettre de les modifier depuis l'éditeur selon le niveau généré spécifiquement et pour potentiellement générer plusieurs ensembles de paramètres pour un même niveau, selon la météo par exemple.

I then created a procedural skybox shader depending on a day/night cycle. This shader allow the sky, lights and celestial bodies colors, and the stars appearance along time and brightness. I added a custom probe to correctly reflect the lights on the scene nearly without any impact on performance. The light, textures and reflection settings are stored in a file and not in the material itself. Thanks to this technic, we can ajust the light settings in the editor depending on the level we created and save several settings to simulate the weather on this level.  

<p align="center"><img src="https://user-images.githubusercontent.com/36695417/200187511-36906bea-b5ae-4f42-96a7-f8ebe5ff7ccb.gif"></p>
<p align="center">the new day/night cycle with procedural skybox</p>

Enfin, j'ai ajouté tout le post-processing nécessaire en qualité optimale (souvent le maximum) pour tester les performances (profondeur de champ, flou lumineux, occlusion ambiante, ajustement des couleurs, balance de blanc, HDR, brouillard exponentiel carré, vignettage). Celles-ci se sont avérées très bonnes pour une qualité visuelle plus que satisfaisante. L'éditeur de niveau permet donc de générer rapidement et efficacement un terrain et d'y appliquer les textures souhaitées d'après un dessin en pixelart, de gérer les lumières du niveau selon un cycle jour/nuit et la météo (ou non), et de placer des points d'eau sur le terrain généré.

Finally, I added all the necessary post-processing in optimal quality (often maximal quality) to test performances (depth of field, bloom, ambiant occlusion, color ajustment, white balance, HDR, exponential squared fog, vignette). They seemed more than enough to me for that visual quality. Now, the editor allow us to generate a terrain and its texture from a pixelart, manage the level lighting, day/night cycle and weather systel (if needed), and set up water surfaces on the generated terrain.

<p align="center"><img src="https://user-images.githubusercontent.com/36695417/200188356-6ffca4d6-3b1c-4f69-8a47-62ecd604d681.gif"></p>
<p align="center">final result with post-processing</p>

=====================
Version 0.3
=====================

Les textures sont désormais générées selon une image, la texture map. Elles sont extraites d'un tileset composé entre autre d'un set de textures par défaut (ici l'herbe verte et ses variations), de plusieurs variantes de sol (ici l'herbe jaune et la terre avec leurs variations) et des transitions entre deux textures (trois au maximum sur mon tileset, mais rien n'empêche d'en ajouter, le script peut en accepter autant que nécessaire). Les transitions sont des textures transparentes permettant de voir une autre texture de sol en dessous. Le nombre de variations de chaque texture ainsi que leurs chances d'apparition individuelles sont paramétrables dans le script "Texture Manager".

The textures are now generated from a texture map. They are extracted from a tileset, containing a set of the default texture (the green grass and its variants here), 
a set of other ground textures (like yellow grass, dirt and their variants), and some transition textures (3 in my tileset, but you can add as many of them as you like). The last of them are textures with alpha component, so you can see another texture throught it. The number of variants and the drop rate for each texture is manageable in the "Texture Manager" script.

<p align="center"><img src="https://user-images.githubusercontent.com/36695417/196054308-95bde081-22b8-4082-8cf0-4381f96ea905.png"></p>
<p align="center">the texture map</p>

<p align="center"><img src="https://user-images.githubusercontent.com/36695417/196054360-642a2046-61bf-4719-827a-9ecd84e9f98e.png"></p>
<p align="center">and the terrain generated from it</p>

Une fois le terrain généré, il est possible de sélectionner les tuiles une par une et de changer l'orientation de la texture, ou d'y appliquer une variante aléatoire de la texture qui s'y trouve. Pour changer le type de sol, le meilleur moyen est encore de modifier directement la texture map.

Once the terrain is generated, you can select tiles one by one, and change their texture rotation or apply a corresponding variant. If you want to change the ground texture, just change the texture map.

<p align="center"><img src="https://user-images.githubusercontent.com/36695417/196054599-ba394e07-1633-4352-8d30-c3115a476329.gif"></p>
<p align="center">the new per tile options</p>

Enfin, on peut manuellement fusionner l'intégralité des meshs des tuiles en un seul, sauvegardé dans les dossiers du projet. Cela permet dans un premier temps de modifier le terrain à la main si besoin, en rajoutant des détails, en modifiant des textures etc... Puis on fusionne le tout, et on obtient non seulement un gain conséquent de performances, mais également un mesh complet que l'on peut retoucher sur un logiciel de modélisation.

Then, we can merge all the meshes manually, and save the result in the project files. So you can generate your terrain, modify some textures if needed, add details, and finally merge everything in a single mesh. You can edit this mesh later with your favorite 3D computer graphics software. Moreover, you can save a bunch of performance this way.

<p align="center"><img src="https://user-images.githubusercontent.com/36695417/196054890-6c6c855a-5013-4db8-b9ee-0867f8baf26f.gif"></p>
<p align="center">the new meshes merging process</p>

============
Version 0.2
============

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
