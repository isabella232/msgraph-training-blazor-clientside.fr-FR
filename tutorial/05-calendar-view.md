---
ms.openlocfilehash: 33bdb86a4a4af997c8ca522e23ec2f883fdeda88
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584622"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="02d0b-101">Dans cette section, vous allez intégrer Microsoft Graph dans l’application pour obtenir une vue du calendrier de l’utilisateur pour la semaine en cours.</span><span class="sxs-lookup"><span data-stu-id="02d0b-101">In this section you will further incorporate Microsoft Graph into the application to get a view of the user's calendar for the current week.</span></span>

## <a name="get-a-calendar-view"></a><span data-ttu-id="02d0b-102">Obtenir un affichage Calendrier</span><span class="sxs-lookup"><span data-stu-id="02d0b-102">Get a calendar view</span></span>

1. <span data-ttu-id="02d0b-103">Créez un fichier dans le répertoire **./pages** nommé **Calendar. Razor** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="02d0b-103">Create a new file in the **./Pages** directory named **Calendar.razor** and add the following code.</span></span>

    ```razor
    @page "/calendar"
    @using Microsoft.Graph
    @using TimeZoneConverter

    @inject GraphTutorial.Graph.GraphClientFactory clientFactory

    <AuthorizeView>
        <Authorized>
            <!-- Temporary JSON dump of events -->
            <code>@graphClient.HttpProvider.Serializer.SerializeObject(events)</code>
        </Authorized>
        <NotAuthorized>
            <RedirectToLogin />
        </NotAuthorized>
    </AuthorizeView>

    @code{
        [CascadingParameter]
        private Task<AuthenticationState> authenticationStateTask { get; set; }

        private GraphServiceClient graphClient;
        private IList<Event> events = new List<Event>();
        private string dateTimeFormat;
    }
    ```

1. <span data-ttu-id="02d0b-104">Ajoutez le code suivant à l’intérieur de la `@code{}` section.</span><span class="sxs-lookup"><span data-stu-id="02d0b-104">Add the following code inside the `@code{}` section.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Pages/Calendar.razor" id="GetEventsSnippet":::

    <span data-ttu-id="02d0b-105">Examinez ce que fait ce code.</span><span class="sxs-lookup"><span data-stu-id="02d0b-105">Consider what this code does.</span></span>

    - <span data-ttu-id="02d0b-106">Il obtient le fuseau horaire, le format de date et le format d’heure de l’utilisateur actuel à partir des revendications personnalisées ajoutées à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="02d0b-106">It gets the current user's time zone, date format, and time format from the custom claims added to the user.</span></span>
    - <span data-ttu-id="02d0b-107">Il calcule le début et la fin de la semaine en cours dans le fuseau horaire préféré de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="02d0b-107">It calculates the start and end of the current week in the user's preferred time zone.</span></span>
    - <span data-ttu-id="02d0b-108">Il obtient une vue de calendrier de Microsoft Graph pour la semaine en cours.</span><span class="sxs-lookup"><span data-stu-id="02d0b-108">It gets a calendar view from Microsoft Graph for the current week.</span></span>
        - <span data-ttu-id="02d0b-109">Il inclut l' `Prefer: outlook.timezone` en-tête pour que Microsoft Graph renvoie `start` les `end` Propriétés et dans le fuseau horaire spécifié.</span><span class="sxs-lookup"><span data-stu-id="02d0b-109">It includes the `Prefer: outlook.timezone` header to cause Microsoft Graph to return the `start` and `end` properties in the specified time zone.</span></span>
        - <span data-ttu-id="02d0b-110">Il utilise `Top(50)` pour demander jusqu’à 50 événements dans la réponse.</span><span class="sxs-lookup"><span data-stu-id="02d0b-110">It uses `Top(50)` to request up to 50 events in the response.</span></span>
        - <span data-ttu-id="02d0b-111">Il utilise `Select(u => new {})` pour demander uniquement les propriétés utilisées par l’application.</span><span class="sxs-lookup"><span data-stu-id="02d0b-111">It uses `Select(u => new {})` to request just the properties used by the app.</span></span>
        - <span data-ttu-id="02d0b-112">Il utilise `OrderBy("start/dateTime")` pour trier les résultats par heure de début.</span><span class="sxs-lookup"><span data-stu-id="02d0b-112">It uses `OrderBy("start/dateTime")` to sort the results by start time.</span></span>

1. <span data-ttu-id="02d0b-113">Enregistrez toutes vos modifications et redémarrez l’application.</span><span class="sxs-lookup"><span data-stu-id="02d0b-113">Save all of your changes and restart the app.</span></span> <span data-ttu-id="02d0b-114">Choisissez l’élément de navigation **calendrier** .</span><span class="sxs-lookup"><span data-stu-id="02d0b-114">Choose the **Calendar** nav item.</span></span> <span data-ttu-id="02d0b-115">L’application affiche une représentation JSON des événements renvoyés par Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="02d0b-115">The app displays a JSON representation of the events returned from Microsoft Graph.</span></span>

## <a name="display-the-results"></a><span data-ttu-id="02d0b-116">Afficher les résultats</span><span class="sxs-lookup"><span data-stu-id="02d0b-116">Display the results</span></span>

<span data-ttu-id="02d0b-117">À présent, vous pouvez remplacer le vidage JSON par un utilisateur plus convivial.</span><span class="sxs-lookup"><span data-stu-id="02d0b-117">Now you can replace the JSON dump with something more user-friendly.</span></span>

1. <span data-ttu-id="02d0b-118">Ajoutez la fonction suivante dans la `@code{}` section.</span><span class="sxs-lookup"><span data-stu-id="02d0b-118">Add the following function inside the `@code{}` section.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Pages/Calendar.razor" id="FormatDateSnippet":::

    <span data-ttu-id="02d0b-119">Ce code prend une chaîne de date ISO 8601 et la convertit au format de date et d’heure préféré de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="02d0b-119">This code takes an ISO 8601 date string and converts it into the user's preferred date and time format.</span></span>

1. <span data-ttu-id="02d0b-120">Remplacez l' `<code>` élément à l’intérieur de l' `<Authorized>` élément par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="02d0b-120">Replace the `<code>` element inside the `<Authorized>` element with the following.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/Calendar.razor" id="CalendarViewSnippet":::

    <span data-ttu-id="02d0b-121">Cette méthode crée un tableau des événements renvoyés par Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="02d0b-121">This creates a table of the events returned by Microsoft Graph.</span></span>

1. <span data-ttu-id="02d0b-122">Enregistrez vos modifications, puis redémarrez l’application.</span><span class="sxs-lookup"><span data-stu-id="02d0b-122">Save your changes and restart the app.</span></span> <span data-ttu-id="02d0b-123">À présent, la page **Calendar** affiche un tableau d’événements.</span><span class="sxs-lookup"><span data-stu-id="02d0b-123">Now the **Calendar** page renders a table of events.</span></span>

    ![Capture d’écran de l’application illustrant un tableau d’événements](images/calendar-view.png)
