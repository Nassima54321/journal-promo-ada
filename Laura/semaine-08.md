# Semaine 8

**What I've learned so far in confinement by myself:**

## Lundi 23 mars

### JavaScript 

Après une semaine solo, j'ai repris les cours JavaScript sur OpenClassroom pour pouvoir organiser tout ce qu'on avait appris,
ça allait plutôt vite vu qu'en cours on à appris à lire les codes, c'est pour pouvoir tout noter dans mon cahier et voir des
notions qu'on avait appris: 

- "Apprenez à programmer avec JavaScript" = 
    - les calculs type `a++=`,
    - les booleens (`true`/`false`), 
    - les fonctions, 
    - la class avec le `constructor` et `this` et la méthode d'instance et les conditions (`if`, `else if`, `else`),
    - l'`array` et les `set` et `map` (qui sont différents type de tableau plus évolué,
    - instruction `switch` avec les `break`
    - la boucle `for` avec `let in` ou `let of`,
      ex: 
      ```JavaScript
            let guestsSeated = 5;
            let seatsReamaining =10;
            let guestsRemaining = 7;
            
            while (seatsRemaining > 0 && guestsRemaining > 0{
              guestsSeated ++;
              seatsReamaining --;
              guestsRemaining --;
             }
        ```
        Dans cet exemple, avant j'avais du mal à comprendre les `++` et les `--` mais ça m'a permis de comprendre en langue 
        française ce que cela donnait si par exemple on demandait la valeur de guestsSeated à la fin de cet extrait? 
        Réponse : 
              `guestsSeated` est initianilisé à 5. La boucle est ensuite exécutée jusqu'à ce que `guestsRemaining` passe à 0 
              (ce qui arrive avant que `seatsRemaining` passe à 0): ce qui ajoute 7 invités, pour un résultat final de 12.
    - la méthodes d'instances à une `class`,
      ex: 
         ```JavaScript
            class Show{
              constructor(title, numberOfSeasons){
                  this.title= title;
                  this.numberOfseasons = numberOfSeasons, 
                  this.ratings = [];
                  this.averageRatings = 0;
                }
                addRating(rating){
                  this.ratings.push(rating);
                  let sum = 0
                  for (let rating of this.ratings){
                  sum +- rating;
                  this.averageRating = sum / this.ratings.length;
         ```
     - la méthode statiques
     - refactoriser du code
     
- "Écrivez du JavaScript pour le web" = 
     - ce qu'est un service web et le protocole HTTP, requête HTTP,
     - rappel du DOM (ex: 
        ```JavaScript
            document.querySelector.getElementByID
                                               Tagg
                                               ClassName
         ```
                                            )
     - comment le modifier avec `get` et `removeAttribute`
     - comment empêcher le comportement par défat avec `event.preventDefault()`
                                                            `.stropPropagation()` // empeche autres éléments de recevoir l'event
     - Ajax (asynchronous JavaScript and XML) qui est un ensemble d'objets et de fonctions 
        ex: 
          ```JavaScript
              var request = new XMLHttpRequest(); //la on créer un nouvel objet XML .. = objet AJAX
              request.open ("GET", "http://url-service-web.com/api/users"); // la on demande ouvrir connexion vers le service web
              request.send(); //on envoie la requête
          ```
     - récupérer les données au format JSON (JavaScript Object Notation) qui est un format plus léger par rapport au XML donc
        plus rapide 
        ex:
            ```JavaScript
           var request = new XMLHttpRequest();
           request.on readystatechange = function{
              if(this.readyState == XMLHttpRequest.DONE && this.status == 200){
                    var response = JSON.parse (this.responseText)
                    console.log (response.current_condition);
              }
           }
            ```
                onreadystatechange = pour récupérer l'etat actuel de la requête 
                readyState = contient l'état de la requête 
                DONE = une fois que la requête est terminé
                status = contient code de status 
                JSON.parse = afin de transformer le texte JSON de la repo en objet JavaScript
                responseText = contient réponse du service web au format texte
     - j'ai appris qu'il fallait aussi ensuite valider ces données suite à des évènements DOM
     - les contraintes HTML avec l'attribut type (bon refresh) ="email" avec min/max,required, min lenght
     - les patterns 
     - envoyer des données avec une requête POST via Ajax 
         ex:
            ```JavaScript
            var request = new XMLHttpRequest();
            request.open ("POST", "http://url-service-web.com/api/users");
            request.setRequestHeader("Content-Type", "application/json");
            request.send (JSON.stringify (jsonBody));
            ```    
           1.JSON.stringify(json = on veut envoyer du JSON a notre service web il faut donc transformer notre objet JavaScript en JSON
           2. Pcq l'on veut envoyer du JSON a notre service web, il faut le prévenir qu'il va recevoir du JSON, grace hearder et il faut donc ajouter cette ligne: request.setRequestHeader ("content-type", "application/json");
                
     - les fonctions asynchrones, 
        - avec l'event loop : la fonction setTimeout étant la plus répandue 2 paramètres: la fonction à exécuter et le délai 
              ex:
              ```JavaScript
                  setTimeout(function(){
                    console.log("I"m here!)
                    }, 5000)                   // délai en milliseconde avant d'éxécuter la fonction 
                  console.log ("Where are you");
                ```
        - avec la fonction `cleanTimeout` et les autres méthode moins répandue avec `setInterval` ou `setImmediate` et l'I/O 
        - avec la gestion `callback = fonction` qui sera exécuté par une autre fonction lorsque cette dernière aura terminé
     - les promises (+puissant + facile a lire)
          ex: 
            ```JavaScript
              functionThatReturnAPromise()
                .then(function(data){
                })
                .catch(function(err){
                }):
             ```
         l'avantage étant de pouvoir chainer les Promises 
     - la gestion Async/Await (plus intuitive, bloc exécution until result) merci Yannick là d'ailleurs pour l'explication 
          ex:
            ```JavaScript
                async function func1(){
                    return 3;
                }
                async function func2(){
                    return 4;
                }
                var promiseRes = Promise
                    .all ([func1(), func2()])
                    .then (functiion (resultats){
                                return results.reduce (function (acc, res){
                                return acc * res;
                            }, 2);
                    })
                    .then (function(time){
                        return setTimeout (callback, time * 1000);
                    });
              ```
            1. en langage humain ca donne qu'on a 2 fonctions asynchrones en parallèle avec Promise.all 
            2. le premier then appelle reduce sur la liste resultat (donc 3 et 4) et les multiplie avec la valeur initiale 2
                (check MDN pour réduce, c'est juste comme cela que ca s'écrit) 
            3. le résultat précédent 24 = time va être appelé avec callback apres 
            4. promiseRes vaut une promesse résolue avec l'identifiant de la fonction setTimeout et la callback est appelé
                après 24 sec.

### Ce que j'ai appris en HTML/ CSS pour projet Codevores 

(Ayant fait JavaScript pendant 5 jours, j'ai commencé le projet Codevores samedi)

#### 1. J'ai donc fait du benchmark toute la journée pour trouver de l'insipiration et j'ai trouvé ces sites utiles :

- https://www.webascender.com/blog/10-places-to-look-for-website-design-inspiration/?fbclid=IwAR2wLVnj5Zg1j-EZ-JG4pqQ5nIs3GkUv1SMQs0yg5n9hxVlkmEwclV6InGU
- https://www.awwwards.com/
- https://www.webdesign-inspiration.com/fr/webdesign/style/colore

#### 2. Puis j'ai fait une maquette pour savoir si je remplissais tout les critères du cahier des charges, en dessinant à peu 
près toutes les pages dont j'avais besoin. 

#### 3. J'ai passé mon temps à copier coller les codes des autres sites à chaque fois qu'une animation ou une mise en page m'intéréssait 

#### 4. Ce que j'ai appris : 

- Faire de l'animation en CSS avec :
```css
.paragraphs p{
  font-size: 1.25rem;
  line-height: 1.5;
  text-align: justify;
  animation-duration: 3s;
  animation-name: slidein;
}

@keyframes slidein {
  from {
    margin-left: 150%;
    width: 300%;
  }

  to {
    margin-left: 50%;
    width: 100%;
  }
}
```

Cela fait slider mon paragraph à chaque actualisation et avec MDN j'ai vu qu'on pouvait le faire en illimité 

- Faire du responsive avec cette vidéo : https://www.youtube.com/watch?v=Up_NC-qGzuI

- l'importance de noter ce qu'on veut faire sur un post it pour ne pas perdre sa concentration, à force de vagabonder de site 
  en site, on finit par en oublier qu'on doit faire le projet haha 


## Mardi 24

### HTML / CSS

- apprendre à faire du responsive façon Hell'vyra: 
    1. aller sur la console, cliquer sur le petit bouton ipad/iphone 
    2. changer dans la console le titre h1 par exemple puis le rétrécir a la bonne taille 
    3. le changer dans Atom avec @media screen and (max-width:375px){ commencer en mobile first pour que ce sois plus facile après
    4. elle nous a aussi appris a bien indenter, ex:
                                            (max-width:375px){
                                                                    .link-dev {

                                                                                padding-left: 0em;
                                                                    }

                                                                    .inscription .codevores{

                                                                                display: none;
                                                                    }
                                                                    .accroche h1{

                                                                                font-size: 1em;
                                                                    }
     5. Note pour soi même et ne pas prendre la flemme: s'habituer au responsive car très demander sur le marché et on 
        devra souvent justement reprendre des sites non adapté au responsive 
        
- ce que j'ai appris par moi-même hier en visitant des sites web: 
     1. faire encore plus d'animation haha ex: 
                                                  #list-animation {
                                                    margin: 2em auto;
                                                    padding: 0;
                                                    max-width: 600px;
                                                    list-style: none;
                                                    overflow: scroll;
                                                  }

                                                  #list-animation li {
                                                    display:inline-block;
                                                    width: 10em;
                                                    height: 12em;
                                                    margin: 3em 1em;
                                                    text-align: center;
                                                    line-height: 2em;
                                                    opacity: 0;
                                                    animation: fadeIn 1s ease-in both;
                                                  }

                                                  #list-animation li:nth-child(2) {
                                                    animation-delay: 1s;
                                                  }
                                                  #list-animation li:nth-child(3) {
                                                    animation-delay: 2s;
                                                  }
                                                  #list-animation li:nth-child(4) {
                                                    animation-delay: 3s;
                                                  }
                                                  #list-animation li:nth-child(5) {
                                                    animation-delay: 4s;
                                                  }
                                                  #list-animation li:nth-child(5) {
                                                    animation-delay: 5s;
                                                  }
                                                  #list-animation li:nth-child(5) {
                                                    animation-delay: 5s;
                                                  }
          Cela permet de faire "glisser" ma liste ul li (moi j'ai mis des screenshots de portfolio cliquable) petit
          à petit :) 
          
       2.Grâce à Yannick j'ai aussi appris qu'il fallait éviter de mettre des heights partout parce que du coup, 
          certaines partis se superposent sinon, et qu'il valait mieux mettre overflow hidden/scroll! 
          
PS: j'ai voulu reproduire cette figure mais je n'ai pas eu le temps de bien me mettre à l'intérieur pour tout comprendre mais 
quand j'aurai le temps j'aimerai bien que l'on m'explique cette petite figure et comment ca marche:

              <!--  POUR LE FUN

                <h5 id="ember469" class="scratch __styled-h__9e9ec ember-view">
                  <span>   We are present all over the world on every continent, just pick your location!</span>

                    <svg viewBox="0 0 1535 276">
                      <path class="stroke-1" d="M51 90L145 43C145 64 59 184 66 197C73.4057 210.753 241 63 269 58C269 58 164 202 178 232C183.092 242.912 394 74 394 74C366.333 128.667 287 232 307 232C327 232 460.333 133.667 538 74C475 137.667 408.4 241.2 454 226C499.6 210.8 708 57 744 52L611 208L860 74" stroke="#1C25FF" stroke-width="20" stroke-linecap="round" stroke-linejoin="round"></path>
                      <path class="stroke-2" d="M58.0083 81.2929C48.9737 90.0731 39.3106 113.524 33.999 122.446C30.4637 128.384 29.7796 133.55 30.2023 139.384C30.2462 139.99 30.1624 144.84 31.3324 144.708C37.9221 143.966 53.694 130.14 58.0083 127.668C80.7342 114.645 104.296 101.475 130.408 89.3927C137.215 86.243 150.762 80.8554 161.453 81.2929C167.625 81.5454 147.257 94.2916 145.728 95.3921C129.648 106.964 115.5 119.351 102.564 131.401C84.5556 148.174 74.0285 166.663 65.4448 184.078C61.87 191.332 64.6638 198.98 65.1792 206.093C65.9766 217.098 80.06 200.833 82.8491 198.295C110.485 173.153 157.255 149.086 199.377 127.052C234.295 108.787 268.963 89.8599 311.851 74.3207C328.608 68.2492 346.278 61.4512 367.447 58.3694C373.411 57.5011 377.388 56.3602 373.895 60.0498C360.177 74.5408 332.754 87.235 310.551 100.038C260.537 128.879 225.059 160.123 198.162 192.458C187.115 205.739 170.883 221.287 171.091 234.855C171.107 235.912 174.068 246.617 181.62 241.497C230.257 208.526 281.834 175.884 336.633 144.138C384.919 116.165 437.386 87.1268 499.379 63.6215C526.612 53.296 554.699 37.9558 587.606 30.6426C597.968 28.3398 595.486 35.2589 595.174 37.5C592.685 55.3725 569.855 73.7661 550.635 90.4932C507.364 128.152 445.954 161.872 398.077 198.635C379.71 212.739 363.424 229.572 366.063 244.722C366.849 249.235 382.968 238.807 383.655 238.412C423.809 215.287 465.571 192.77 508.796 170.47C572.555 137.575 641.353 103.945 716.984 75.1078C726.197 71.5949 767.492 55.9037 771.099 66.9656C775.396 80.1465 753.416 96.4795 739.335 108.813C710.26 134.281 683.212 159.632 661.001 185.88C658.258 189.121 627.424 220.999 644.79 224.083C669.096 228.398 728.631 194.864 738.675 189.583C797.218 158.8 824 127.668 904 100.038" stroke="#2727E6" stroke-width="60" stroke-linecap="round" stroke-linejoin="round"></path>
                    </svg>
                </h5> -->

/* POUR LE FUN
h5 {
    animation: fadein .6s cubic-bezier(.165,.84,.44,1) both;
    position: relative;
}
*/
