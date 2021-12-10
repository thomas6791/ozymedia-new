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
## Créer un Datalayer ou accéder au DataLayer existant {#creer-datalyer}
{% highlight js %}
<script>
  dataLayer = window.dataLayer || [];
  console.log(datalayer); // visualiser dans la console son dataLayer
</script>
{% endhighlight %}

### Exemple de dataLayer Ecommerce
{% highlight js %}
<script>
  dataLayer = window.dataLayer || [];
  dataLayer.push({
    'event': 'myevent', // mise en place de mon événement
    "ecommerce": {
      "purchase": {
        "actionField": {
          "id": "123456",
          "affiliation": "Outdoor Adventure Park",
          "revenue": "29.98",
          "location": "Bristol"
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
  dataLayer = window.dataLayer || [];
  dataLayer.push({'event': 'mynewEvent'});
</script>
{% endhighlight %}
<br><br>
<img src="/assets/images/posts/articles/evenement-personnalise-gtm.jpg" width="100%">
<br><br>
On peut maintenant utiliser cet évenement comme trigger(déclencheur)
<br><br>
<img src="/assets/images/posts/articles/declencheur-personnalise-gtm.jpg" width="100%">
## Ajouter une nouvelle variable à son DataLayer
Si la variable déclarée n'existe pas à l'emplacement voulu, celle-ci y est ajoutée
{% highlight js %}
<script>
  dataLayer = window.dataLayer || [];
  dataLayer.push({'ecommerce':{'purchase' :{ 'actionField' :{'newitem': 'my new value'}}}});
</script>
{% endhighlight %}

Ce qui donne :
{% highlight js %}
  dataLayer = window.dataLayer || [];
  dataLayer.push({
    'event': 'monEvenementPersonnalise',
    "ecommerce": {
      "purchase": {
        "actionField": {
          "id": "123456",
          "affiliation": "Outdoor Adventure Park",
          "revenue": "29.98",
          "location": "Bristol",
          "newitem": "my new value" // Notre nouvelle valeur se trouve dans l'objet purchase
        },
        ...
{% endhighlight %}
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
Pour par exemple stocker le nom du second produit(Clay Pigeons) de notre dataLayer dans une variable "dlv - productName".
{% highlight js %}
ecommerce.purchase.products.1.name
{% endhighlight %}

#### Utiliser une variable de javascript personnalisée
Pour récupérer la *localisation* de l'élément *actionField*, il nous faut d'abord créer une variable de couche de données pour nous faciliter un peu le travail.
<br>Je créer donc une variable de couche de données plutôt simple en récupérant uniquement les données ecommerce > purchase du DataLayser.<br>
Je nomme cette variable : *dlv - ecommerce purchase datas*
{% highlight js %}
ecommerce.purchase
{% endhighlight %}
<br>
A présent je créer une variable Javascript Personnalisée que je nomme *dlv - purchase location*.
<pre>
  <code>
  function(){
    return &#x7B;&#x7B;dlv - ecommerce purchase datas&#x7d;&#x7d;.actionField.location;
  }
  </code>
</pre>


## Modifier les valeurs de son DataLayer
On souhaite mettre à jour la valeur "Bristol" dans notre DataLayer par "New York"
Dans une balise HTML de GTM on intègre le script suivant
{% highlight js %}
<script>
  dataLayer.push({'ecommerce':{'purchase':{ 'actionField':{'location':"New York"}}}});
</script>
{% endhighlight %}
