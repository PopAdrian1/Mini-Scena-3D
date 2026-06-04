# Mini Scena 3D

O simulare 3D în browser unde lansezi o rachetă în spațiu.

## Cum funcționează

Ține apăsat W ca să zbori. Dai drumul la W ca să te oprești.
Trage cu mouse-ul ca să rotești scena.

## Ce există în scenă

- Rachetă cu corp, nas, fereastră, aripioare și motor
- Platformă de lansare cu turn suport
- Flacără la motor din 8 conuri care pulsează (generata de AI)
- 2 planete — albastră și verde
- 5000 de stele în fundal (generate de AI)

## Tehnologii

- Three.js  pentru grafică 3D


Am creat o scenă care simulează lansarea unei rachete în spațiu.

Racheta este formată din mai multe forme geometrice. Pentru corp am folosit un cilindru, pentru vârf și motor câte un con. Fiecare formă folosește `MeshPhongMaterial` — un material care reacționează la lumină.

Flacăra motorului și fundalul cu stele a fost realizat folosind AI. Flacăra este formată din mai multe conuri puțin suprapuse și de culori diferite care sunt afișate când apăsăm "W" să lansăm racheta. Conurile folosesc `MeshBasicMaterial` cu `AdditiveBlending` — culorile se adună între ele și dau un efect de strălucire.

Platforma este formată dintr-un paralelipiped dreptunghic (`BoxGeometry`). Pe platformă este pus un stâlp de susținere pentru rachetă, aceasta fiind poziționată puțin deasupra platformei.

Camera privește întotdeauna la rachetă și o urmărește.

Scena are trei tipuri de lumini: `AmbientLight` care iluminează tot uniform, `DirectionalLight` care vine dintr-o direcție ca soarele, și `PointLight` lângă motorul rachetei care strălucește când zbori.

Planetele sunt niște sfere poziționate la diferite înălțimi, au diferite raze și sunt poziționate la poziții diferite pe axa x pentru a da volum scenei.

Viteza este setată la 0.55. Asta înseamnă că atunci când apăsăm "W", y_racheta = y_racheta + viteză. Când eliberăm tasta, viteza este setată automat la 0.

Animația rulează cu `requestAnimationFrame`, care execută bucla de ~60 ori pe secundă. Timpul scurs este urmărit cu `clock.getElapsedTime()` și este folosit pentru mișcări periodice precum pulsatul flăcării.

Când tragi cu mouse-ul, nu se mișcă camera ci toată scena se rotește în jurul ei. Tot ce există — racheta, planetele, stelele, platforma — e pus într-un grup numit `worldGroup`. Când tragi, rotim acel grup pe X și Y, iar camera rămâne fixă pe loc.

