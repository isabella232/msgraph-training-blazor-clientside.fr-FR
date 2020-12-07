---
ms.openlocfilehash: 723f1d08b9d1085d47d0d5fac71da5371badc3d0
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584540"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="8129d-101">Dans cette section, vous allez ajouter la possibilité de créer des événements dans le calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8129d-101">In this section you will add the ability to create events on the user's calendar.</span></span>

1. <span data-ttu-id="8129d-102">Créez un fichier dans le répertoire **./pages** nommé **NewEvent. Razor** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="8129d-102">Create a new file in the **./Pages** directory named **NewEvent.razor** and add the following code.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/NewEvent.razor" id="NewEventFormSnippet":::

    <span data-ttu-id="8129d-103">Cette opération ajoute un formulaire à la page afin que l’utilisateur puisse entrer des valeurs pour le nouvel événement.</span><span class="sxs-lookup"><span data-stu-id="8129d-103">This adds a form to the page so the user can enter values for the new event.</span></span>

1. <span data-ttu-id="8129d-104">Ajoutez le code suivant à la fin du fichier.</span><span class="sxs-lookup"><span data-stu-id="8129d-104">Add the following code to the end of the file.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/NewEvent.razor" id="NewEventCodeSnippet":::

    <span data-ttu-id="8129d-105">Examinez ce que fait ce code.</span><span class="sxs-lookup"><span data-stu-id="8129d-105">Consider what this code does.</span></span>

    - <span data-ttu-id="8129d-106">`OnInitializedAsync`Il obtient le fuseau horaire de l’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="8129d-106">In `OnInitializedAsync` it gets the authenticated user's time zone.</span></span>
    - <span data-ttu-id="8129d-107">Dans `CreateEvent` celui-ci, un nouvel objet **Event** est initialisé à l’aide des valeurs du formulaire.</span><span class="sxs-lookup"><span data-stu-id="8129d-107">In `CreateEvent` it initializes a new **Event** object using the values from the form.</span></span>
    - <span data-ttu-id="8129d-108">Il utilise le kit de développement logiciel Graph pour ajouter l’événement au calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8129d-108">It uses the Graph SDK to add the event to the user's calendar.</span></span>

1. <span data-ttu-id="8129d-109">Enregistrez toutes vos modifications et redémarrez l’application.</span><span class="sxs-lookup"><span data-stu-id="8129d-109">Save all of your changes and restart the app.</span></span> <span data-ttu-id="8129d-110">Sur la page **calendrier** , sélectionnez **nouvel événement**.</span><span class="sxs-lookup"><span data-stu-id="8129d-110">On the **Calendar** page, select **New event**.</span></span> <span data-ttu-id="8129d-111">Renseignez le formulaire, puis choisissez **créer**.</span><span class="sxs-lookup"><span data-stu-id="8129d-111">Fill in the form and choose **Create**.</span></span>

    ![Capture d’écran du nouveau formulaire d’événement](images/create-event.png)
