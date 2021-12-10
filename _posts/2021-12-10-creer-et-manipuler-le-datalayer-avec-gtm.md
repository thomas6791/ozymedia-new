---
layout: post
author: Thomas Hunckler
poste : Expert SEO
tags: ["GTM"]
lang: fr
permalink: blog/creer-et-manipuler-un-datalayer-avec-gtm
title: Créer et manipuler un datalayer avec Google Tag Manager
titre: Créer et manipuler un datalayer avec Google Tag Manager
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
Récupérer l'array qui a pour event "monEvenementPersonnalise".

{% highlight js %}
  var array = dataLayer.filter(item => (item.event === "monEvenementPersonnalise"));
  console.log(array);
  //[{…}]
  //  0:
  //  ecommerce: {purchase: {…}}
  //  event: "monEvenementPersonnalise"
  //  gtm.uniqueEventId: 4
  //  [[Prototype]]: Object
  //  length: 1
  //[[Prototype]]: Array(0)
{% endhighlight %}

Accéder à la valeur de location avec l'exemple ci-dessus :

{% highlight js %}
  var array = dataLayer.filter(item => (item.event === "monEvenementPersonnalise"));
  var location = array[0].ecommerce.purchase.actionField.location;
{% endhighlight %}

### Récupérer sa variable via GTM

Pour récupérer les données souhaitées via Google Tag Manager on peut soit définir une variable avec du Javascript personnalisé ou en utilisant les variables de couche de données.

#### Récupérer via les variables de couche de données
Pour par exemple stocker le nom du second produit(Clay Pigeons) de notre dataLayer dans une variable dlv - productName par exemple.
{% highlight js %}
ecommerce.purchase.products.1.name
{% endhighlight %}

#### Utiliser une variable de javascript personnalisée

## Modifier les valeurs de son DataLayer
On souhaite mettre à jour la valeur "Bristol" dans notre DataLayer par "New York"
Dans une balise HTML de GTM on intègre le script suivant
{% highlight js %}
<script>
  dataLayer.push({'ecommerce':{'purchase' :{ 'actionField' :{'location': "New York"}}}});
</script>
{% endhighlight %}
