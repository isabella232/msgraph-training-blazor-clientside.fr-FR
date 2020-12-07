---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584539"
---
<a name="open-iconic-v111"></a>[Ouvrir emblématique v 1.1.1](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconic-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collection"></a>Open emblématique est le frère Open source de [emblématique](http://useiconic.com). Il s’agit d’une collection hyper-lisible d’icônes 223 avec un petit encombrement &mdash; prêt à être utilisé avec bootstrap et Foundation. [Afficher la collection](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a>Qu’est-ce que le emblématique Open ?

* 223 icônes conçues pour être lisibles jusqu’à 8 pixels
* Fichiers SVG Super-Light-61,8 pour l’ensemble du jeu 
* SVG-Sprite &mdash; moderne de remplacement des polices d’icône
* Formats webfont (EOT, OTF, SVG, TTF, WOFF), PNG et WebP
* Feuilles de style webfont (y compris les versions pour bootstrap et Foundation) en CSS, moins, SCSS et les formats stylet
* Images de trame PNG et WebP dans 8PX, 16px, des, des, 48px et 64px.


## <a name="getting-started"></a>Prise en main

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-icons-and-reference-sections"></a>Pour obtenir des exemples de code et tout ce dont vous avez besoin pour commencer à utiliser Open emblématique, consultez nos [icônes](http://useiconic.com/open#icons) et les sections de [référence](http://useiconic.com/open#reference) .

### <a name="general-usage"></a>Utilisation générale

#### <a name="using-open-iconics-svgs"></a>Utilisation de l’emblématique d’ouvrir SVGs

Nous souhaitons que SVGs et nous pensons qu’il s’agit de la façon d’afficher des icônes sur le Web. Étant donné que les emblématique d’ouverture sont simplement des SVGs de base, nous vous suggérons de les afficher comme vous le feriez pour toute autre image (n’oubliez pas l' `alt` attribut).

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a>Utilisation de l’emblématique SVG d’Open

Open emblématique est également fourni dans un sprite SVG qui vous permet d’afficher toutes les icônes du jeu en une seule requête. Il s’agit d’une police d’icône, sans être un pirate.

L’ajout d’une icône d’un sprite SVG est légèrement différent de celui que vous utilisez, mais c’est toujours un élément de gâteau. *Conseil : pour que vos icônes soient facilement stylistiques, nous vous recommandons d’ajouter une classe générale au* `<svg>` *et un nom de classe unique pour chaque icône dans le* `<use>` *balise.*  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

Les icônes de dimensionnement n’ont besoin que CSS de base. Toutes les icônes sont en format carré, c’est pourquoi il suffit de définir la `<svg>` balise avec des dimensions de largeur et de hauteur égales.

```
.icon {
  width: 16px;
  height: 16px;
}
```

La coloration des icônes est encore plus facile. Tout ce que vous avez à faire est de définir la `fill` règle sur la `<use>` balise.

```
.icon-account-login {
  fill: #f00;
}
```

Pour en savoir plus sur les sprites SVG, consultez le [Guide de Chris Coyier](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).

#### <a name="using-open-iconics-icon-font"></a>Utilisation de la police d’icône de l’emblématique Open...


##### <a name="with-bootstrap"></a>... avec bootstrap

Vous trouverez nos feuilles de style de démarrage dans `font/css/open-iconic-bootstrap.{css, less, scss, styl}`


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a>... avec base

Vous trouverez nos feuilles de style de base dans `font/css/open-iconic-foundation.{css, less, scss, styl}`

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a>... de sa propre

Vous trouverez nos feuilles de style par défaut dans `font/css/open-iconic.{css, less, scss, styl}`

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a>Licence

### <a name="icons"></a>Icônes

Tout le code (y compris les balises SVG) est sous la [licence MIT](http://opensource.org/licenses/MIT).

### <a name="fonts"></a>Polices

Toutes les polices sont sous [licence sil](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).
