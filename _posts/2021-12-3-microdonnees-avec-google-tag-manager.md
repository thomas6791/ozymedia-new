---
layout: post
author: thomas
titre: Comment intégrer des microdonnées avec Google Tag Manager ?
---
Comment intégrer des microdonnées avec Google Tag Manager ?

## Installer Google Tag Manager

## Installer un schema de base avec Google Tag Manager

## Le problème des macros et l'absence de variables dans son schema

### Comment résoudre le problème des macros
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
