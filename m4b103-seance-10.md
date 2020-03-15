---
description: poursuite de la séance du 3 mars (App mobile)
---

# M4B103-seance-10 \(16 mars 11h\)

### Exercice 1: Remise à plat de la partie front

Nous considérerons que la partie boussole fonctionne. voir la video de correction:

### Exercice 2: Gestion du timer avec le bouton d'activation du traker

pour l'instant nous allons tester la gestion de la sauvegarde des coordonnées GPS quand on active le bouton "traquer" \(dans le fichier index.html\). 

```text
...
traquer <input type="checkbox" id="traker"> 
...
```



![](.gitbook/assets/img_8922.jpg)

### mise en place de la sauvegarde toute les 30s \(mettre 5s pour les tests\)

faite un timer \(toutes les 30s\) qui enverra au final les coordonnées GPS vers votre serveur.

utiliser :

```text
var i=0;
setInterval(function(){
    $('#zoneinfo').html("ça marche :"+i);
    i++;
},5000);


```

vérifiez bien que votre timer fonctionne en lui faisant écrire dans une zone "texte" de votre application. Ici toute les 5s, on va écrire l'état de la checkbox dans la zone de text \#zoneinfo

```text
setInterval(function(){

    $$('#zoneinfo').html( $$('#traker').prop('checked') );

},10000);
```

une fois que cela fonctionne \(et uniquement si cela fonctionne! ça ne sert à rien d'aller plus loin si cela ne fonctionne pas\), afficher "sauvegarde activé" ou "sauvegarde désactivé" dans la zone de texte \#zoneinfo.

```text
setInterval(function(){
    if($$('#traker').prop('checked')........) {
        $$('#zoneinfo')...;
        }
    else {
        $$('#zoneinfo')....;
        }
},5000);
```

### Récupération des coordonnees GPS toute les 30s \(5s pour vos tests\)

en utilisant le source suivant, vous pouvez récupérer les coordonnées GPS et les afficher dans votre zone \#zoneinfo mais le faire uniquement si la checkbox est True.

```text
setInterval(function(){
    if($$('#traker').prop('checked')........) {
        navigator.geolocation.getCurrentPosition(maPosition);
        }
    else {
        $$('#zoneinfo')...."sauvegarde désactivée" ... ;
        }
},5000);

function maPosition(position) {
    var lat = position.coords.latitude;
    var long = position.coords.longitude;
    $$('#zoneinfo')... lat ... long ... ;
    }
```

vous devez donc voir apparaitre vos coordonnées dans la zone \#zoneinfo mais uniquement si la chekbox est activée.

### Sauvegarde des coordonnées dans la base de données.

pour cela vous pouvez appeler votre API de mise à jours de la table coordonnées. ou au moins pour faire vos tests appeler "http://MONIP/mmitraceur/save.php?longitude=48.5423&latitude=4.6432&iduser=1". Dans ce cas, faites le fichier save.php qui sauve ces infos dans votre table coordonnées. 

Nous allons ici travailler sans l'API \(nous reprendons la version API plus tard\)

pour envoyer les datas vous pouvez utiliser:

```text
...
Framework7.request.get('http://149....82/mmiTrack/save.php?longi=48...&lat=...&id=1', function(data) {...});
...
```

ajouter un checkbox sur votre appli mobile pour activer ou non la sauvegarde des coordonnées GPS vers votre VPS

![](.gitbook/assets/img_8922.jpg)

testez la valeur de ce bouton dans votre timer



```text
setInterval(function(){
  navigator.geolocation.getCurrentPosition(maPosition);

},30000);

function maPosition(position) {

//...
console.log();
}
```

