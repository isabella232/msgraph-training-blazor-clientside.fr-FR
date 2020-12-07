---
ms.openlocfilehash: 744df064e4fdc1bbf7821ae43a7b7878148902e9
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584615"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="cacb0-101">Commencez par créer une application de webassembly éblouissante.</span><span class="sxs-lookup"><span data-stu-id="cacb0-101">Start by creating a Blazor WebAssembly app.</span></span>

1. <span data-ttu-id="cacb0-102">Ouvrez votre interface de ligne de commande (CLI) dans un répertoire où vous souhaitez créer le projet.</span><span class="sxs-lookup"><span data-stu-id="cacb0-102">Open your command-line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="cacb0-103">Exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="cacb0-103">Run the following command.</span></span>

    ```Shell
    dotnet new blazorwasm --auth SingleOrg -o GraphTutorial
    ```

    <span data-ttu-id="cacb0-104">Le `--auth SingleOrg` paramètre fait en sorte que le projet généré inclue la configuration d’authentification avec la plateforme d’identité Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cacb0-104">The `--auth SingleOrg` parameter causes the generated project to include configuration for authentication with the Microsoft identity platform.</span></span>

1. <span data-ttu-id="cacb0-105">Une fois le projet créé, vérifiez qu’il fonctionne en remplaçant le répertoire actuel par le répertoire **GraphTutorial** et en exécutant la commande suivante dans votre CLI.</span><span class="sxs-lookup"><span data-stu-id="cacb0-105">Once the project is created, verify that it works by changing the current directory to the **GraphTutorial** directory and running the following command in your CLI.</span></span>

    ```Shell
    dotnet watch run
    ```

1. <span data-ttu-id="cacb0-106">Ouvrez votre navigateur et accédez à `https://localhost:5001` .</span><span class="sxs-lookup"><span data-stu-id="cacb0-106">Open your browser and browse to `https://localhost:5001`.</span></span> <span data-ttu-id="cacb0-107">Si tout fonctionne, vous devez voir un « Hello, World ! ».</span><span class="sxs-lookup"><span data-stu-id="cacb0-107">If everything is working, you should see a "Hello, world!"</span></span> <span data-ttu-id="cacb0-108">Message.</span><span class="sxs-lookup"><span data-stu-id="cacb0-108">message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cacb0-109">Si vous recevez un avertissement indiquant que le certificat de **localhost** n’est pas approuvé, vous pouvez utiliser l’infrastructure CLI .net pour installer et approuver le certificat de développement.</span><span class="sxs-lookup"><span data-stu-id="cacb0-109">If you receive a warning that the certificate for **localhost** is un-trusted you can use the .NET Core CLI to install and trust the development certificate.</span></span> <span data-ttu-id="cacb0-110">Pour obtenir des instructions sur des systèmes d’exploitation spécifiques, voir [Enforce https in ASP.net Core](/aspnet/core/security/enforcing-ssl?view=aspnetcore-3.1) .</span><span class="sxs-lookup"><span data-stu-id="cacb0-110">See [Enforce HTTPS in ASP.NET Core](/aspnet/core/security/enforcing-ssl?view=aspnetcore-3.1) for instructions for specific operating systems.</span></span>

## <a name="add-nuget-packages"></a><span data-ttu-id="cacb0-111">Ajouter des packages NuGet</span><span class="sxs-lookup"><span data-stu-id="cacb0-111">Add NuGet packages</span></span>

<span data-ttu-id="cacb0-112">Avant de poursuivre, installez des packages NuGet supplémentaires que vous utiliserez plus tard.</span><span class="sxs-lookup"><span data-stu-id="cacb0-112">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="cacb0-113">[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) pour effectuer des appels Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="cacb0-113">[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) for making calls to Microsoft Graph.</span></span>
- <span data-ttu-id="cacb0-114">[TimeZoneConverter](https://github.com/mj1856/TimeZoneConverter) pour la traduction des identificateurs de fuseau horaire Windows en identificateurs IANA.</span><span class="sxs-lookup"><span data-stu-id="cacb0-114">[TimeZoneConverter](https://github.com/mj1856/TimeZoneConverter) for translating Windows time zone identifiers to IANA identifiers.</span></span>

1. <span data-ttu-id="cacb0-115">Exécutez les commandes suivantes dans votre interface CLI pour installer les dépendances.</span><span class="sxs-lookup"><span data-stu-id="cacb0-115">Run the following commands in your CLI to install the dependencies.</span></span>

    ```Shell
    dotnet add package Microsoft.Graph --version 3.18.0
    dotnet add package TimeZoneConverter
    ```

## <a name="design-the-app"></a><span data-ttu-id="cacb0-116">Concevoir l’application</span><span class="sxs-lookup"><span data-stu-id="cacb0-116">Design the app</span></span>

<span data-ttu-id="cacb0-117">Dans cette section, vous allez créer la structure de base de l’interface utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="cacb0-117">In this section you will create the basic UI structure of the application.</span></span>

1. <span data-ttu-id="cacb0-118">Supprimez les exemples de pages générés par le modèle.</span><span class="sxs-lookup"><span data-stu-id="cacb0-118">Remove sample pages generated by the template.</span></span> <span data-ttu-id="cacb0-119">Supprimez les fichiers suivants.</span><span class="sxs-lookup"><span data-stu-id="cacb0-119">Delete the following files.</span></span>

    - <span data-ttu-id="cacb0-120">**./Pages/Counter.razor**</span><span class="sxs-lookup"><span data-stu-id="cacb0-120">**./Pages/Counter.razor**</span></span>
    - <span data-ttu-id="cacb0-121">**./Pages/FetchData.razor**</span><span class="sxs-lookup"><span data-stu-id="cacb0-121">**./Pages/FetchData.razor**</span></span>
    - <span data-ttu-id="cacb0-122">**./Shared/SurveyPrompt.razor**</span><span class="sxs-lookup"><span data-stu-id="cacb0-122">**./Shared/SurveyPrompt.razor**</span></span>
    - <span data-ttu-id="cacb0-123">**weather.js./wwwroot/Sample-Data/sur**</span><span class="sxs-lookup"><span data-stu-id="cacb0-123">**./wwwroot/sample-data/weather.json**</span></span>

1. <span data-ttu-id="cacb0-124">Ouvrez **/wwwroot/index.html** et ajoutez le code suivant juste **avant** la `</body>` balise de fermeture.</span><span class="sxs-lookup"><span data-stu-id="cacb0-124">Open **./wwwroot/index.html** and add the following code just **before** the closing `</body>` tag.</span></span>

    :::code language="html" source="../demo/GraphTutorial/wwwroot/index.html" id="BootStrapJSSnippet":::

    <span data-ttu-id="cacb0-125">Cela ajoute les fichiers de [démarrage](https://getbootstrap.com/docs/4.5/getting-started/introduction/) JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cacb0-125">This adds the [Bootstrap](https://getbootstrap.com/docs/4.5/getting-started/introduction/) javascript files.</span></span>

1. <span data-ttu-id="cacb0-126">Ouvrez **./wwwroot/CSS/App.CSS** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="cacb0-126">Open **./wwwroot/css/app.css** and add the following code.</span></span>

    :::code language="css" source="../demo/GraphTutorial/wwwroot/css/app.css" id="CssSnippet":::

1. <span data-ttu-id="cacb0-127">Ouvrez **./Shared/NavMenu.Razor** et remplacez son contenu par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="cacb0-127">Open **./Shared/NavMenu.razor** and replace its contents with the following.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Shared/NavMenu.razor" id="NavMenuSnippet":::

1. <span data-ttu-id="cacb0-128">Ouvrez **./pages/index.Razor** et remplacez son contenu par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="cacb0-128">Open **./Pages/Index.razor** and replace its contents with the following.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/Index.razor" id="IndexSnippet":::

1. <span data-ttu-id="cacb0-129">Ouvrez **./Shared/LoginDisplay.Razor** et remplacez son contenu par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="cacb0-129">Open **./Shared/LoginDisplay.razor** and replace its contents with the following.</span></span>

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

1. <span data-ttu-id="cacb0-130">Créez un répertoire dans le répertoire **./wwwroot** nommé **img**.</span><span class="sxs-lookup"><span data-stu-id="cacb0-130">Create a new directory in the **./wwwroot** directory named **img**.</span></span> <span data-ttu-id="cacb0-131">Ajoutez un fichier image de votre choix nommé **no-profile-photo.png** dans ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="cacb0-131">Add an image file of your choosing named **no-profile-photo.png** in this directory.</span></span> <span data-ttu-id="cacb0-132">Cette image sera utilisée comme photo de l’utilisateur lorsque l’utilisateur n’aura pas de photo dans Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="cacb0-132">This image will be used as the user's photo when the user has no photo in Microsoft Graph.</span></span>

    > [!TIP]
    > <span data-ttu-id="cacb0-133">Vous pouvez télécharger l’image utilisée dans ces captures d’écran à partir de [GitHub](https://github.com/microsoftgraph/msgraph-training-blazor-clientside/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png).</span><span class="sxs-lookup"><span data-stu-id="cacb0-133">You can download the image used in these screenshots from [GitHub](https://github.com/microsoftgraph/msgraph-training-blazor-clientside/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png).</span></span>

1. <span data-ttu-id="cacb0-134">Enregistrez toutes vos modifications et actualisez la page.</span><span class="sxs-lookup"><span data-stu-id="cacb0-134">Save all of your changes and refresh the page.</span></span>

    ![Capture d’écran de la page d’accueil repensée](./images/create-app-01.png)
