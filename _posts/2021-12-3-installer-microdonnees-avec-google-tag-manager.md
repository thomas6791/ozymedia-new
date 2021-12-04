---
layout: post
author: thomas
permalink: installer-microdonnees-avec-google-tag-manager
titre: Comment intégrer des microdonnées avec Google Tag Manager ?
---
## Installer un schema de microdonnées au format JSON-LD avec Google Tag Manager
Intégrer des microdonnées sur son site permet aux moteurs de recherche et notamment à Google de mieux comprendre les informations présents sur une page et d'afficher des SERPS plus riches.
Avec ces microdonnées il est donc possible d'améliorer son taux de clic en ayant affiché par exemple ses avis.
### Le schema classique des microdonnées
Les différents schemas de microdonnées selon les informations que vous voulez intégrer au format Json se trouvent sur le site [schema.org](https://schema.org/).
On intégrera ici le format JSON-LD qui est ici plus simple à implémenter via GTM que par les Microdata.
D'ailleurs Google a une légère préférence pour le format JSON-LD avec lequel il a davantage de facilité de lecture.

### Implémenter le schema en intégrant des variables dynamiques
Pour ajouter un schema de microdonnées avec Google Tag Manager :<br>
1. Créez une "nouvelle balise" avec comme type de balise "HTML Personnalisée"<br>
2. Ajoutez comme déclencheur "All Pages"


#### Créer quelques variables dynamiques dans Google Tag Manager

#### Les intégrer dans son schema

#### Mes variables dynamiques ne remontent pas


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
