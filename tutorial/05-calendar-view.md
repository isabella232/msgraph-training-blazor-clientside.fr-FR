---
ms.openlocfilehash: 33bdb86a4a4af997c8ca522e23ec2f883fdeda88
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584622"
---
<!-- markdownlint-disable MD002 MD041 -->

Dans cette section, vous allez intégrer Microsoft Graph dans l’application pour obtenir une vue du calendrier de l’utilisateur pour la semaine en cours.

## <a name="get-a-calendar-view"></a>Obtenir un affichage Calendrier

1. Créez un fichier dans le répertoire **./pages** nommé **Calendar. Razor** et ajoutez le code suivant.

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

1. Ajoutez le code suivant à l’intérieur de la `@code{}` section.

    :::code language="csharp" source="../demo/GraphTutorial/Pages/Calendar.razor" id="GetEventsSnippet":::

    Examinez ce que fait ce code.

    - Il obtient le fuseau horaire, le format de date et le format d’heure de l’utilisateur actuel à partir des revendications personnalisées ajoutées à l’utilisateur.
    - Il calcule le début et la fin de la semaine en cours dans le fuseau horaire préféré de l’utilisateur.
    - Il obtient une vue de calendrier de Microsoft Graph pour la semaine en cours.
        - Il inclut l' `Prefer: outlook.timezone` en-tête pour que Microsoft Graph renvoie `start` les `end` Propriétés et dans le fuseau horaire spécifié.
        - Il utilise `Top(50)` pour demander jusqu’à 50 événements dans la réponse.
        - Il utilise `Select(u => new {})` pour demander uniquement les propriétés utilisées par l’application.
        - Il utilise `OrderBy("start/dateTime")` pour trier les résultats par heure de début.

1. Enregistrez toutes vos modifications et redémarrez l’application. Choisissez l’élément de navigation **calendrier** . L’application affiche une représentation JSON des événements renvoyés par Microsoft Graph.

## <a name="display-the-results"></a>Afficher les résultats

À présent, vous pouvez remplacer le vidage JSON par un utilisateur plus convivial.

1. Ajoutez la fonction suivante dans la `@code{}` section.

    :::code language="csharp" source="../demo/GraphTutorial/Pages/Calendar.razor" id="FormatDateSnippet":::

    Ce code prend une chaîne de date ISO 8601 et la convertit au format de date et d’heure préféré de l’utilisateur.

1. Remplacez l' `<code>` élément à l’intérieur de l' `<Authorized>` élément par ce qui suit.

    :::code language="razor" source="../demo/GraphTutorial/Pages/Calendar.razor" id="CalendarViewSnippet":::

    Cette méthode crée un tableau des événements renvoyés par Microsoft Graph.

1. Enregistrez vos modifications, puis redémarrez l’application. À présent, la page **Calendar** affiche un tableau d’événements.

    ![Capture d’écran de l’application illustrant un tableau d’événements](images/calendar-view.png)
