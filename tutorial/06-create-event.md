---
ms.openlocfilehash: 723f1d08b9d1085d47d0d5fac71da5371badc3d0
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584540"
---
<!-- markdownlint-disable MD002 MD041 -->

Dans cette section, vous allez ajouter la possibilité de créer des événements dans le calendrier de l’utilisateur.

1. Créez un fichier dans le répertoire **./pages** nommé **NewEvent. Razor** et ajoutez le code suivant.

    :::code language="razor" source="../demo/GraphTutorial/Pages/NewEvent.razor" id="NewEventFormSnippet":::

    Cette opération ajoute un formulaire à la page afin que l’utilisateur puisse entrer des valeurs pour le nouvel événement.

1. Ajoutez le code suivant à la fin du fichier.

    :::code language="razor" source="../demo/GraphTutorial/Pages/NewEvent.razor" id="NewEventCodeSnippet":::

    Examinez ce que fait ce code.

    - `OnInitializedAsync`Il obtient le fuseau horaire de l’utilisateur authentifié.
    - Dans `CreateEvent` celui-ci, un nouvel objet **Event** est initialisé à l’aide des valeurs du formulaire.
    - Il utilise le kit de développement logiciel Graph pour ajouter l’événement au calendrier de l’utilisateur.

1. Enregistrez toutes vos modifications et redémarrez l’application. Sur la page **calendrier** , sélectionnez **nouvel événement**. Renseignez le formulaire, puis choisissez **créer**.

    ![Capture d’écran du nouveau formulaire d’événement](images/create-event.png)
