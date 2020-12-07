---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584539"
---
<a name="open-iconic-v111"></a>[<span data-ttu-id="99937-101">Ouvrir emblématique v 1.1.1</span><span class="sxs-lookup"><span data-stu-id="99937-101">Open Iconic v1.1.1</span></span>](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconic-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collection"></a><span data-ttu-id="99937-102">Open emblématique est le frère Open source de [emblématique](http://useiconic.com).</span><span class="sxs-lookup"><span data-stu-id="99937-102">Open Iconic is the open source sibling of [Iconic](http://useiconic.com).</span></span> <span data-ttu-id="99937-103">Il s’agit d’une collection hyper-lisible d’icônes 223 avec un petit encombrement &mdash; prêt à être utilisé avec bootstrap et Foundation.</span><span class="sxs-lookup"><span data-stu-id="99937-103">It is a hyper-legible collection of 223 icons with a tiny footprint&mdash;ready to use with Bootstrap and Foundation.</span></span> [<span data-ttu-id="99937-104">Afficher la collection</span><span class="sxs-lookup"><span data-stu-id="99937-104">View the collection</span></span>](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a><span data-ttu-id="99937-105">Qu’est-ce que le emblématique Open ?</span><span class="sxs-lookup"><span data-stu-id="99937-105">What's in Open Iconic?</span></span>

* <span data-ttu-id="99937-106">223 icônes conçues pour être lisibles jusqu’à 8 pixels</span><span class="sxs-lookup"><span data-stu-id="99937-106">223 icons designed to be legible down to 8 pixels</span></span>
* <span data-ttu-id="99937-107">Fichiers SVG Super-Light-61,8 pour l’ensemble du jeu</span><span class="sxs-lookup"><span data-stu-id="99937-107">Super-light SVG files - 61.8 for the entire set</span></span> 
* <span data-ttu-id="99937-108">SVG-Sprite &mdash; moderne de remplacement des polices d’icône</span><span class="sxs-lookup"><span data-stu-id="99937-108">SVG sprite&mdash;the modern replacement for icon fonts</span></span>
* <span data-ttu-id="99937-109">Formats webfont (EOT, OTF, SVG, TTF, WOFF), PNG et WebP</span><span class="sxs-lookup"><span data-stu-id="99937-109">Webfont (EOT, OTF, SVG, TTF, WOFF), PNG and WebP formats</span></span>
* <span data-ttu-id="99937-110">Feuilles de style webfont (y compris les versions pour bootstrap et Foundation) en CSS, moins, SCSS et les formats stylet</span><span class="sxs-lookup"><span data-stu-id="99937-110">Webfont stylesheets (including versions for Bootstrap and Foundation) in CSS, LESS, SCSS and Stylus formats</span></span>
* <span data-ttu-id="99937-111">Images de trame PNG et WebP dans 8PX, 16px, des, des, 48px et 64px.</span><span class="sxs-lookup"><span data-stu-id="99937-111">PNG and WebP raster images in 8px, 16px, 24px, 32px, 48px and 64px.</span></span>


## <a name="getting-started"></a><span data-ttu-id="99937-112">Prise en main</span><span class="sxs-lookup"><span data-stu-id="99937-112">Getting Started</span></span>

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-icons-and-reference-sections"></a><span data-ttu-id="99937-113">Pour obtenir des exemples de code et tout ce dont vous avez besoin pour commencer à utiliser Open emblématique, consultez nos [icônes](http://useiconic.com/open#icons) et les sections de [référence](http://useiconic.com/open#reference) .</span><span class="sxs-lookup"><span data-stu-id="99937-113">For code samples and everything else you need to get started with Open Iconic, check out our [Icons](http://useiconic.com/open#icons) and [Reference](http://useiconic.com/open#reference) sections.</span></span>

### <a name="general-usage"></a><span data-ttu-id="99937-114">Utilisation générale</span><span class="sxs-lookup"><span data-stu-id="99937-114">General Usage</span></span>

#### <a name="using-open-iconics-svgs"></a><span data-ttu-id="99937-115">Utilisation de l’emblématique d’ouvrir SVGs</span><span class="sxs-lookup"><span data-stu-id="99937-115">Using Open Iconic's SVGs</span></span>

<span data-ttu-id="99937-116">Nous souhaitons que SVGs et nous pensons qu’il s’agit de la façon d’afficher des icônes sur le Web.</span><span class="sxs-lookup"><span data-stu-id="99937-116">We like SVGs and we think they're the way to display icons on the web.</span></span> <span data-ttu-id="99937-117">Étant donné que les emblématique d’ouverture sont simplement des SVGs de base, nous vous suggérons de les afficher comme vous le feriez pour toute autre image (n’oubliez pas l' `alt` attribut).</span><span class="sxs-lookup"><span data-stu-id="99937-117">Since Open Iconic are just basic SVGs, we suggest you display them like you would any other image (don't forget the `alt` attribute).</span></span>

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a><span data-ttu-id="99937-118">Utilisation de l’emblématique SVG d’Open</span><span class="sxs-lookup"><span data-stu-id="99937-118">Using Open Iconic's SVG Sprite</span></span>

<span data-ttu-id="99937-119">Open emblématique est également fourni dans un sprite SVG qui vous permet d’afficher toutes les icônes du jeu en une seule requête.</span><span class="sxs-lookup"><span data-stu-id="99937-119">Open Iconic also comes in a SVG sprite which allows you to display all the icons in the set with a single request.</span></span> <span data-ttu-id="99937-120">Il s’agit d’une police d’icône, sans être un pirate.</span><span class="sxs-lookup"><span data-stu-id="99937-120">It's like an icon font, without being a hack.</span></span>

<span data-ttu-id="99937-121">L’ajout d’une icône d’un sprite SVG est légèrement différent de celui que vous utilisez, mais c’est toujours un élément de gâteau.</span><span class="sxs-lookup"><span data-stu-id="99937-121">Adding an icon from an SVG sprite is a little different than what you're used to, but it's still a piece of cake.</span></span> <span data-ttu-id="99937-122">*Conseil : pour que vos icônes soient facilement stylistiques, nous vous recommandons d’ajouter une classe générale au* `<svg>` *et un nom de classe unique pour chaque icône dans le* `<use>` *balise.*</span><span class="sxs-lookup"><span data-stu-id="99937-122">*Tip: To make your icons easily style able, we suggest adding a general class to the* `<svg>` *tag and a unique class name for each different icon in the* `<use>` *tag.*</span></span>  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

<span data-ttu-id="99937-123">Les icônes de dimensionnement n’ont besoin que CSS de base.</span><span class="sxs-lookup"><span data-stu-id="99937-123">Sizing icons only needs basic CSS.</span></span> <span data-ttu-id="99937-124">Toutes les icônes sont en format carré, c’est pourquoi il suffit de définir la `<svg>` balise avec des dimensions de largeur et de hauteur égales.</span><span class="sxs-lookup"><span data-stu-id="99937-124">All the icons are in a square format, so just set the `<svg>` tag with equal width and height dimensions.</span></span>

```
.icon {
  width: 16px;
  height: 16px;
}
```

<span data-ttu-id="99937-125">La coloration des icônes est encore plus facile.</span><span class="sxs-lookup"><span data-stu-id="99937-125">Coloring icons is even easier.</span></span> <span data-ttu-id="99937-126">Tout ce que vous avez à faire est de définir la `fill` règle sur la `<use>` balise.</span><span class="sxs-lookup"><span data-stu-id="99937-126">All you need to do is set the `fill` rule on the `<use>` tag.</span></span>

```
.icon-account-login {
  fill: #f00;
}
```

<span data-ttu-id="99937-127">Pour en savoir plus sur les sprites SVG, consultez le [Guide de Chris Coyier](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span><span class="sxs-lookup"><span data-stu-id="99937-127">To learn more about SVG Sprites, read [Chris Coyier's guide](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span></span>

#### <a name="using-open-iconics-icon-font"></a><span data-ttu-id="99937-128">Utilisation de la police d’icône de l’emblématique Open...</span><span class="sxs-lookup"><span data-stu-id="99937-128">Using Open Iconic's Icon Font...</span></span>


##### <a name="with-bootstrap"></a><span data-ttu-id="99937-129">... avec bootstrap</span><span class="sxs-lookup"><span data-stu-id="99937-129">…with Bootstrap</span></span>

<span data-ttu-id="99937-130">Vous trouverez nos feuilles de style de démarrage dans `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="99937-130">You can find our Bootstrap stylesheets in `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span></span>


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a><span data-ttu-id="99937-131">... avec base</span><span class="sxs-lookup"><span data-stu-id="99937-131">…with Foundation</span></span>

<span data-ttu-id="99937-132">Vous trouverez nos feuilles de style de base dans `font/css/open-iconic-foundation.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="99937-132">You can find our Foundation stylesheets in `font/css/open-iconic-foundation.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a><span data-ttu-id="99937-133">... de sa propre</span><span class="sxs-lookup"><span data-stu-id="99937-133">…on its own</span></span>

<span data-ttu-id="99937-134">Vous trouverez nos feuilles de style par défaut dans `font/css/open-iconic.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="99937-134">You can find our default stylesheets in `font/css/open-iconic.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a><span data-ttu-id="99937-135">Licence</span><span class="sxs-lookup"><span data-stu-id="99937-135">License</span></span>

### <a name="icons"></a><span data-ttu-id="99937-136">Icônes</span><span class="sxs-lookup"><span data-stu-id="99937-136">Icons</span></span>

<span data-ttu-id="99937-137">Tout le code (y compris les balises SVG) est sous la [licence MIT](http://opensource.org/licenses/MIT).</span><span class="sxs-lookup"><span data-stu-id="99937-137">All code (including SVG markup) is under the [MIT License](http://opensource.org/licenses/MIT).</span></span>

### <a name="fonts"></a><span data-ttu-id="99937-138">Polices</span><span class="sxs-lookup"><span data-stu-id="99937-138">Fonts</span></span>

<span data-ttu-id="99937-139">Toutes les polices sont sous [licence sil](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span><span class="sxs-lookup"><span data-stu-id="99937-139">All fonts are under the [SIL Licensed](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span></span>
