---
layout: post
author: Thomas Hunckler
poste : Expert SEO
tags: ["GTM"]
lang: fr
permalink: blog/creer-et-manipuler-le-datalayer-avec-gtm
title: Créer et manipuler le datalayer avec Google Tag Manager
titre: Créer et manipuler le datalayer avec Google Tag Manager
---
## Créer un Datalayer ou accéder ou DataLayer existant {#creer-datalyer}
{% highlight js %}
  <script>
    window.dataLayer = window.dataLayer || [];
    console.log(datalayer); // visualiser dans la console son dataLayer
  </script>
{% endhighlight %}

### Exemple de dataLayer Ecommerce
{% highlight js %}
<script>
  window.dataLayer = window.dataLayer || [];
  dataLayer.push({
    'event': 'monEvenementPersonnalise',
    "ecommerce": {
      "purchase": {
        "actionField": {
          "id": "123456",
          "affiliation": "Outdoor Adventure Park",
          "revenue": "29.98",
          "location": "Bristol" // Our custom purchase attribute
        },
        "products": [{
          "name": "Quad Biking",
          "id": "15727899",
          "category": "Vehicle Track",
          "price": "14.99",
          "quantity": "1"
        },
        {
          "name": "Clay Pigeons",
          "id": "16682710",
          "category": "Shooting Range",
          "price": "14.99",
          "quantity": "1"
        }]
      }
    }
  });
</script>
{% endhighlight %}

## Pousser un événement personnalisé dans son DataLayer
{% highlight js %}
  <script>
    window.dataLayer = window.dataLayer || [];
    dataLayer.push({'event': 'monEvenementPersonnalise'});
  </script>
{% endhighlight %}

## Ajouter une nouvelle variable à son DataLayer

## Accéder à une variable

### Récupérer sa variable avec du javascript

### Récupérer sa variable via GTM

## Modifier les valeurs de son DataLayer
On souhaite mettre à jour la valeur "Bristol" dans notre DataLayer par "New York"
Dans une balise HTML de GTM on intègre le script suivant
{% highlight js %}
<script>
  dataLayer.push({'ecommerce':{'purchase' :{ 'actionField' :{'location': "New York"}}}});
</script>
{% endhighlight %}
