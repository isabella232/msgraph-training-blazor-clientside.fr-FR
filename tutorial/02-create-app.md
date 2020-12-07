---
ms.openlocfilehash: 744df064e4fdc1bbf7821ae43a7b7878148902e9
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584615"
---
<!-- markdownlint-disable MD002 MD041 -->

Commencez par créer une application de webassembly éblouissante.

1. Ouvrez votre interface de ligne de commande (CLI) dans un répertoire où vous souhaitez créer le projet. Exécutez la commande suivante.

    ```Shell
    dotnet new blazorwasm --auth SingleOrg -o GraphTutorial
    ```

    Le `--auth SingleOrg` paramètre fait en sorte que le projet généré inclue la configuration d’authentification avec la plateforme d’identité Microsoft.

1. Une fois le projet créé, vérifiez qu’il fonctionne en remplaçant le répertoire actuel par le répertoire **GraphTutorial** et en exécutant la commande suivante dans votre CLI.

    ```Shell
    dotnet watch run
    ```

1. Ouvrez votre navigateur et accédez à `https://localhost:5001` . Si tout fonctionne, vous devez voir un « Hello, World ! ». Message.

> [!IMPORTANT]
> Si vous recevez un avertissement indiquant que le certificat de **localhost** n’est pas approuvé, vous pouvez utiliser l’infrastructure CLI .net pour installer et approuver le certificat de développement. Pour obtenir des instructions sur des systèmes d’exploitation spécifiques, voir [Enforce https in ASP.net Core](/aspnet/core/security/enforcing-ssl?view=aspnetcore-3.1) .

## <a name="add-nuget-packages"></a>Ajouter des packages NuGet

Avant de poursuivre, installez des packages NuGet supplémentaires que vous utiliserez plus tard.

- [Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) pour effectuer des appels Microsoft Graph.
- [TimeZoneConverter](https://github.com/mj1856/TimeZoneConverter) pour la traduction des identificateurs de fuseau horaire Windows en identificateurs IANA.

1. Exécutez les commandes suivantes dans votre interface CLI pour installer les dépendances.

    ```Shell
    dotnet add package Microsoft.Graph --version 3.18.0
    dotnet add package TimeZoneConverter
    ```

## <a name="design-the-app"></a>Concevoir l’application

Dans cette section, vous allez créer la structure de base de l’interface utilisateur de l’application.

1. Supprimez les exemples de pages générés par le modèle. Supprimez les fichiers suivants.

    - **./Pages/Counter.razor**
    - **./Pages/FetchData.razor**
    - **./Shared/SurveyPrompt.razor**
    - **weather.js./wwwroot/Sample-Data/sur**

1. Ouvrez **/wwwroot/index.html** et ajoutez le code suivant juste **avant** la `</body>` balise de fermeture.

    :::code language="html" source="../demo/GraphTutorial/wwwroot/index.html" id="BootStrapJSSnippet":::

    Cela ajoute les fichiers de [démarrage](https://getbootstrap.com/docs/4.5/getting-started/introduction/) JavaScript.

1. Ouvrez **./wwwroot/CSS/App.CSS** et ajoutez le code suivant.

    :::code language="css" source="../demo/GraphTutorial/wwwroot/css/app.css" id="CssSnippet":::

1. Ouvrez **./Shared/NavMenu.Razor** et remplacez son contenu par ce qui suit.

    :::code language="razor" source="../demo/GraphTutorial/Shared/NavMenu.razor" id="NavMenuSnippet":::

1. Ouvrez **./pages/index.Razor** et remplacez son contenu par ce qui suit.

    :::code language="razor" source="../demo/GraphTutorial/Pages/Index.razor" id="IndexSnippet":::

1. Ouvrez **./Shared/LoginDisplay.Razor** et remplacez son contenu par ce qui suit.

    ```razor
    @using Microsoft.AspNetCore.Components.Authorization
    @using Microsoft.AspNetCore.Components.WebAssembly.Authentication

    @inject NavigationManager Navigation
    @inject SignOutSessionStateManager SignOutManager

    <AuthorizeView>
        <Authorized>
            <a class="text-decoration-none" data-toggle="dropdown" href="#" role="button">
                <img src="/img/no-profile-photo.png" class="nav-profile-photo rounded-circle align-self-center mr-2">
            </a>
            <div class="dropdown-menu dropdown-menu-right">
                <h5 class="dropdown-item-text mb-0">@context.User.Identity.Name</h5>
                <p class="dropdown-item-text text-muted mb-0">placeholder@contoso.com</p>
                <div class="dropdown-divider"></div>
                <button class="dropdown-item" @onclick="BeginLogout">Log out</button>
            </div>
        </Authorized>
        <NotAuthorized>
            <a href="authentication/login">Log in</a>
        </NotAuthorized>
    </AuthorizeView>

    @code{
        private async Task BeginLogout(MouseEventArgs args)
        {
            await SignOutManager.SetSignOutState();
            Navigation.NavigateTo("authentication/logout");
        }
    }
    ```

1. Créez un répertoire dans le répertoire **./wwwroot** nommé **img**. Ajoutez un fichier image de votre choix nommé **no-profile-photo.png** dans ce répertoire. Cette image sera utilisée comme photo de l’utilisateur lorsque l’utilisateur n’aura pas de photo dans Microsoft Graph.

    > [!TIP]
    > Vous pouvez télécharger l’image utilisée dans ces captures d’écran à partir de [GitHub](https://github.com/microsoftgraph/msgraph-training-blazor-clientside/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png).

1. Enregistrez toutes vos modifications et actualisez la page.

    ![Capture d’écran de la page d’accueil repensée](./images/create-app-01.png)
