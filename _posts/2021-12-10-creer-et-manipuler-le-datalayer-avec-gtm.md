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

## Mettre à jour les variables de son DataLayer
test
{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}
