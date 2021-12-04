---
layout: post
author: thomas
permalink: installer-microdonnees-avec-google-tag-manager
titre: Comment intégrer des microdonnées avec Google Tag Manager ?
---
## Installer un schema de microdonnées au format JSON-LD avec Google Tag Manager
Intégrer des microdonnées sur son site permet aux moteurs de recherche dont Google, de mieux comprendre les informations présents sur une page et d'afficher des SERP plus riches.<br>
Bien que l'**intégration de ces microdonnées** n'apporte pas encore de gains dans le positionnement de ses pages, ces microdonnées permettent d'occuper un peu plus l'espace dans les résultats et d'attirer davantage l'oeil de l'internaute en affichant par exemple les avis ou le prix de sa page produit. Ces éléments augmentent le taux de clic sur ses pages<br>
<br>
Le problème est que les référenceurs ou les responsables marketing ont rarement les compétences ou la main pour intégrer un script directement sur leur site ou pour installer un module qui ne donne pas les résultats escomptés.<br><br>
Une des solutions pour gagner en indépendance et en efficacité est de passer par l'**intégration de ces microdonnées par Google Tag Manager**.<br>
Pourtant Google Tag Manager apporte avec lui quelques surprises lorsque l'on essaye d'intégrer des variables dynamiques à ses **microdatas**.
### Le schema classique des microdonnées
Les différents schemas de microdonnées selon les informations que vous voulez intégrer au format Json se trouvent sur le site [schema.org](https://schema.org/).
On intégrera ici le format JSON-LD qui est ici plus simple à implémenter via GTM que par les Microdata.
D'ailleurs Google a une légère préférence pour le format JSON-LD avec lequel il a davantage de facilité de lecture.

### Implémenter le schema en intégrant des variables dynamiques
Pour ajouter un schema de microdonnées avec Google Tag Manager :<br>
1. Créez une "nouvelle balise" avec comme type "HTML Personnalisée"<br>
2. Intégrer un script incluant un schema de ce type :<br>
<pre>
  <code>
  &lt;script type="application/ld+json"&gt;
    {
      "@context": "https://schema.org",
      "@type": "Person",
      "address": {
        "@type": "PostalAddress",
        "addressLocality": "Seattle",
        "addressRegion": "WA",
        "postalCode": "98052",
        "streetAddress": "20341 Whitworth Institute 405 N. Whitworth"
      },
      "colleague": [
        "http://www.xyz.edu/students/alicejones.html",
        "http://www.xyz.edu/students/bobsmith.html"
      ],
      "email": "mailto:jane-doe@xyz.edu",
      "image": "janedoe.jpg",
      "jobTitle": "Professor",
      "name": "Jane Doe",
      "telephone": "(425) 123-4567",
      "url": "http://www.janedoe.com"
    }
  &lt;/script&gt;
  </code>
</pre>
<br>
3. Ajoutez comme déclencheur "All Pages"


#### Créer quelques variables dynamiques dans Google Tag Manager

1. Créez une variable "Javascript Personnalisé"<br>
2. <br>
<pre>
  <code>
    function() {
      var email = document.getElementById("email-address").innerText;
      return email;
    }
  </code>
</pre>


#### Les intégrer dans son schema
Intégrer ma variable ''EMAIL'' et ''Tel Number''
<pre>
  <code>
  &lt;script type="application/ld+json"&gt;
    {
      "@context": "https://schema.org",
      "@type": "Person",
      "address": {
        "@type": "PostalAddress",
        "addressLocality": "Seattle",
        "addressRegion": "WA",
        "postalCode": "98052",
        "streetAddress": "20341 Whitworth Institute 405 N. Whitworth"
      },
      "colleague": [
        "http://www.xyz.edu/students/alicejones.html",
        "http://www.xyz.edu/students/bobsmith.html"
      ],
      "email": "mailto:&#x7B;&#x7B; EMAIL &#x7d;&#x7d;",
      "image": "janedoe.jpg",
      "jobTitle": "Professor",
      "name": "Jane Doe",
      "telephone": "&#x7B;&#x7B; Tel Number &#x7d;&#x7d;",
      "url": "http://www.janedoe.com"
    }
  &lt;/script&gt;
  </code>
</pre>

#### Problème : Mes variables dynamiques ne remontent pas !


## Comment résoudre le problème des macros ?
Afin de régler le problème macro il faut à la fois intégrer l'ensemble du schema dans une variable et générer ce schema microdonnées par l'intégration de méthodes supplémentaires en fin de script.
<pre>
  <code>
    var script = document.createElement('script');
    script.type = "application/ld+json";
    script.innerHTML = JSON.stringify(data);
    document.getElementsByTagName('head')[0].appendChild(script);
  </code>
</pre>
<br>
On créer ensuite une fonction anonyme avec une variable "data" ou l'on intègre son schema de microdonnées
<pre>
  <code>
    var data {
      "@context" : "http://schema.org",
      "@type" : "FoodEstablishment",
      ...
    }
  </code>
</pre>
### Le code complet
<pre>
  <code>
&lt;script&gt;
  (function(){
    var data = {
      "@context" : "http://schema.org",
      "@type" : "FoodEstablishment",
      "name" : "Bernard Cook",
      "location": {
        "@type": "PostalAddress",
        "streetAddress": "10 rue des tilleuls",
        "addressLocality": "OBERMODERN-ZUTZENDORF",
        "postalCode": "67330"
      },
      "areaServed": {
        "@type": "GeoCircle",
        "geoMidpoint": {
            "@type": "GeoCoordinates",
            "latitude": 48.84732437133789,
            "longitude": 7.531085968017578
           },
           "geoRadius": 50000
      },
      "contactPoint" : [
        { "@type" : "ContactPoint",
          "telephone" : "{{TEL NUMBER}}",
          "email" : "mail_to:{{EMAIL}}",
          "contactType" : "customer service"
        } ]
    }
    var script = document.createElement('script');
    script.type = "application/ld+json";
    script.innerHTML = JSON.stringify(data);
    document.getElementsByTagName('head')[0].appendChild(script);
  })(document);
&lt;/script&gt;
</code>
</pre>

Source : https://moz.com/blog/using-google-tag-manager-to-dynamically-generate-schema-org-json-ld-tags
