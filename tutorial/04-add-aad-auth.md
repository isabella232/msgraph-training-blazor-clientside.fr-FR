---
ms.openlocfilehash: f98548a1332417d92b126a2cb7499fea5306b34f
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584580"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="e6ea5-101">Dans cet exercice, vous allez étendre l’application de l’exercice précédent pour prendre en charge l’authentification avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-101">In this exercise you will extend the application from the previous exercise to support authentication with Azure AD.</span></span> <span data-ttu-id="e6ea5-102">Cette opération est obligatoire pour obtenir le jeton d’accès OAuth nécessaire pour appeler l’API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-102">This is required to obtain the necessary OAuth access token to call the Microsoft Graph API.</span></span>

1. <span data-ttu-id="e6ea5-103">Open **./wwwroot/appsettings.js**.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-103">Open **./wwwroot/appsettings.json**.</span></span> <span data-ttu-id="e6ea5-104">Ajoutez une `GraphScopes` propriété et mettez à jour les `Authority` `ClientId` valeurs et pour qu’elles correspondent à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-104">Add a `GraphScopes` property and update the `Authority` and `ClientId` values to match the following.</span></span>

    :::code language="json" source="../demo/GraphTutorial/wwwroot/appsettings.example.json" highlight="3-4,7":::

    <span data-ttu-id="e6ea5-105">Remplacez `YOUR_APP_ID_HERE` par l’ID d’application de l’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-105">Replace `YOUR_APP_ID_HERE` with the application ID from your app registration.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e6ea5-106">Si vous utilisez le contrôle de code source tel que git, il est maintenant recommandé d’exclure le **appsettings.jssur** le fichier à partir du contrôle de code source pour éviter une fuite accidentelle de votre ID d’application.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-106">If you're using source control such as git, now would be a good time to exclude the **appsettings.json** file from source control to avoid inadvertently leaking your app ID.</span></span>

    <span data-ttu-id="e6ea5-107">Examinez les étendues incluses dans la `GraphScopes` valeur.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-107">Review the scopes included in the `GraphScopes` value.</span></span>

    - <span data-ttu-id="e6ea5-108">**User. Read** permet à l’application d’obtenir le profil et la photo de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-108">**User.Read** allows the application to get the user's profile and photo.</span></span>
    - <span data-ttu-id="e6ea5-109">**MailboxSettings. Read** permet à l’application d’obtenir des paramètres de boîte aux lettres, ce qui inclut le fuseau horaire préféré de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-109">**MailboxSettings.Read** allows the application to get mailbox settings, which includes the user's preferred time zone.</span></span>
    - <span data-ttu-id="e6ea5-110">**Calendars. ReadWrite** permet à l’application de lire et d’écrire dans le calendrier de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-110">**Calendars.ReadWrite** allows the application to read and write to the user's calendar.</span></span>

## <a name="implement-sign-in"></a><span data-ttu-id="e6ea5-111">Implémentation de la connexion</span><span class="sxs-lookup"><span data-stu-id="e6ea5-111">Implement sign-in</span></span>

<span data-ttu-id="e6ea5-112">À ce stade, le modèle de projet .NET Core a ajouté le code permettant d’activer la connexion.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-112">At this point the .NET Core project template has added the code to enable sign in.</span></span> <span data-ttu-id="e6ea5-113">Toutefois, dans cette section, vous allez ajouter du code supplémentaire pour améliorer l’expérience en ajoutant des informations de Microsoft Graph à l’identité de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-113">However, in this section you'll add additional code to improve the experience by adding information from Microsoft Graph to the user's identity.</span></span>

1. <span data-ttu-id="e6ea5-114">Ouvrez **./pages/Authentication.Razor** et remplacez son contenu par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-114">Open **./Pages/Authentication.razor** and replace its contents with the following.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/Authentication.razor" id="AuthenticationSnippet":::

    <span data-ttu-id="e6ea5-115">Cette opération remplace le message d’erreur par défaut lorsque la connexion ne parvient pas à afficher un message d’erreur renvoyé par le processus d’authentification.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-115">This replaces the default error message when login fails to display any error message returned by the authentication process.</span></span>

1. <span data-ttu-id="e6ea5-116">Créez un répertoire dans la racine du projet nommé **Graph**.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-116">Create a new directory in the root of the project named **Graph**.</span></span>

1. <span data-ttu-id="e6ea5-117">Créez un fichier dans le répertoire **./Graph** nommé **GraphUserAccountFactory.cs** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-117">Create a new file in the **./Graph** directory named **GraphUserAccountFactory.cs** and add the following code.</span></span>

    ```csharp
    using System.Security.Claims;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Components.WebAssembly.Authentication;
    using Microsoft.AspNetCore.Components.WebAssembly.Authentication.Internal;
    using Microsoft.Extensions.Logging;
    using Microsoft.Graph;

    namespace GraphTutorial.Graph
    {
        // Extends the AccountClaimsPrincipalFactory that builds
        // a user identity from the identity token.
        // This class adds additional claims to the user's ClaimPrincipal
        // that hold values from Microsoft Graph
        public class GraphUserAccountFactory
            : AccountClaimsPrincipalFactory<RemoteUserAccount>
        {
            private readonly IAccessTokenProviderAccessor accessor;
            private readonly ILogger<GraphUserAccountFactory> logger;

            public GraphUserAccountFactory(IAccessTokenProviderAccessor accessor,
                ILogger<GraphUserAccountFactory> logger)
            : base(accessor)
            {
                this.accessor = accessor;
                this.logger = logger;
            }

            public async override ValueTask<ClaimsPrincipal> CreateUserAsync(
                RemoteUserAccount account,
                RemoteAuthenticationUserOptions options)
            {
                // Create the base user
                var initialUser = await base.CreateUserAsync(account, options);

                // If authenticated, we can call Microsoft Graph
                if (initialUser.Identity.IsAuthenticated)
                {
                    try
                    {
                        // Add additional info from Graph to the identity
                        await AddGraphInfoToClaims(accessor, initialUser);
                    }
                    catch (AccessTokenNotAvailableException exception)
                    {
                        logger.LogError($"Graph API access token failure: {exception.Message}");
                    }
                    catch (ServiceException exception)
                    {
                        logger.LogError($"Graph API error: {exception.Message}");
                        logger.LogError($"Response body: {exception.RawResponseBody}");
                    }
                }

                return initialUser;
            }

            private async Task AddGraphInfoToClaims(
                IAccessTokenProviderAccessor accessor,
                ClaimsPrincipal claimsPrincipal)
            {
                // TEMPORARY: Get the token and log it
                var result = await accessor.TokenProvider.RequestAccessToken();

                if (result.TryGetToken(out var token))
                {
                    logger.LogInformation($"Access token: {token.Value}");
                }
            }
        }
    }
    ```

    <span data-ttu-id="e6ea5-118">Cette classe étend la classe **AccountClaimsPrincipalFactory** et remplace la `CreateUserAsync` méthode.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-118">This class extends the **AccountClaimsPrincipalFactory** class and overrides the `CreateUserAsync` method.</span></span> <span data-ttu-id="e6ea5-119">Pour l’instant, cette méthode journalise uniquement le jeton d’accès à des fins de débogage.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-119">For now, this method only logs the access token for debugging purposes.</span></span> <span data-ttu-id="e6ea5-120">Vous allez implémenter les appels Microsoft Graph plus loin dans cet exercice.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-120">You'll implement the Microsoft Graph calls later in this exercise.</span></span>

1. <span data-ttu-id="e6ea5-121">Ouvrez **./Program.cs** et ajoutez les `using` instructions suivantes en haut du fichier.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-121">Open **./Program.cs** and add the following `using` statements at the top of the file.</span></span>

    ```csharp
    using Microsoft.AspNetCore.Components.WebAssembly.Authentication;
    using GraphTutorial.Graph;
    ```

1. <span data-ttu-id="e6ea5-122">À l’intérieur `Main` , remplacez l' `builder.Services.AddMsalAuthentication` appel existant par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-122">Inside `Main`, replace the existing `builder.Services.AddMsalAuthentication` call with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Program.cs" id="AddMsalAuthSnippet":::

    <span data-ttu-id="e6ea5-123">Examinez ce que fait ce code.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-123">Consider what this code does.</span></span>

    - <span data-ttu-id="e6ea5-124">Il charge la valeur de `GraphScopes` à partir de **appsettings.js** et ajoute chaque étendue aux étendues par défaut utilisées par le fournisseur MSAL.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-124">It loads the value of `GraphScopes` from **appsettings.json** and adds each scope to the default scopes used by the MSAL provider.</span></span>
    - <span data-ttu-id="e6ea5-125">Il remplace la fabrique de comptes existante par la classe **GraphUserAccountFactory** .</span><span class="sxs-lookup"><span data-stu-id="e6ea5-125">It replaces the existing account factory with the **GraphUserAccountFactory** class.</span></span>

1. <span data-ttu-id="e6ea5-126">Enregistrez vos modifications, puis redémarrez l’application.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-126">Save your changes and restart the app.</span></span> <span data-ttu-id="e6ea5-127">Utilisez le lien **se connecter** pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-127">Use the **Log in** link to log in.</span></span> <span data-ttu-id="e6ea5-128">Passez en revue et acceptez les autorisations demandées.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-128">Review and accept the requested permissions.</span></span>

1. <span data-ttu-id="e6ea5-129">L’application est actualisée avec un message de bienvenue.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-129">The app refreshes with a welcome message.</span></span> <span data-ttu-id="e6ea5-130">Accédez aux outils de développement de votre navigateur et passez en revue l’onglet de la **console** . L’application journalise le jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-130">Access your browser's developer tools and review the **Console** tab. The app logs the access token.</span></span>

    ![Capture d’écran de la fenêtre outils de développement du navigateur affichant le jeton d’accès](images/access-token.png)

## <a name="get-user-details"></a><span data-ttu-id="e6ea5-132">Obtenir les détails de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="e6ea5-132">Get user details</span></span>

<span data-ttu-id="e6ea5-133">Une fois que l’utilisateur a ouvert une session, vous pouvez obtenir ses informations à partir de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-133">Once the user is logged in, you can get their information from Microsoft Graph.</span></span> <span data-ttu-id="e6ea5-134">Dans cette section, vous allez utiliser les informations de Microsoft Graph pour ajouter des revendications supplémentaires au **ClaimsPrincipal** de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-134">In this section you'll use information from Microsoft Graph to add additional claims to the user's **ClaimsPrincipal**.</span></span>

1. <span data-ttu-id="e6ea5-135">Créez un fichier dans le répertoire **./Graph** nommé **GraphClaimsPrincipalExtensions.cs** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-135">Create a new file in the **./Graph** directory named **GraphClaimsPrincipalExtensions.cs** and add the following code.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/GraphClaimsPrincipalExtensions.cs" id="GraphClaimsExtensionsSnippet":::

    <span data-ttu-id="e6ea5-136">Ce code implémente des méthodes d’extension pour la classe **ClaimsPrincipal** qui vous permettent d’obtenir et de définir des revendications avec des valeurs d’objets Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-136">This code implements extension methods for the **ClaimsPrincipal** class that allow you to get and set claims with values from Microsoft Graph objects.</span></span>

1. <span data-ttu-id="e6ea5-137">Créez un fichier dans le répertoire **./Graph** nommé **BlazorAuthProvider.cs** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-137">Create a new file in the **./Graph** directory named **BlazorAuthProvider.cs** and add the following code.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/BlazorAuthProvider.cs" id="BlazorAuthProviderSnippet":::

    <span data-ttu-id="e6ea5-138">Ce code implémente un fournisseur d’authentification pour le kit de développement logiciel (SDK) Microsoft Graph qui utilise le **IAccessTokenProviderAccessor** fourni par le package **Microsoft. AspNetCore. Components. webassembly. Authentication** pour obtenir des jetons d’accès.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-138">This code implements an authentication provider for the Microsoft Graph SDK that uses the **IAccessTokenProviderAccessor** provided by the **Microsoft.AspNetCore.Components.WebAssembly.Authentication** package to get access tokens.</span></span>

1. <span data-ttu-id="e6ea5-139">Créez un fichier dans le répertoire **./Graph** nommé **GraphClientFactory.cs** et ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-139">Create a new file in the **./Graph** directory named **GraphClientFactory.cs** and add the following code.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/GraphClientFactory.cs" id="GraphClientFactorySnippet":::

    <span data-ttu-id="e6ea5-140">Cette classe crée une **GraphServiceClient** configurée avec le **BlazorAuthProvider**.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-140">This class creates a **GraphServiceClient** configured with the **BlazorAuthProvider**.</span></span>

1. <span data-ttu-id="e6ea5-141">Ouvrez **./Program.cs** et modifiez le **BaseAddress** du nouveau **httpclient** sur `"https://graph.microsoft.com"` .</span><span class="sxs-lookup"><span data-stu-id="e6ea5-141">Open **./Program.cs** and change the **BaseAddress** of the new **HttpClient** to `"https://graph.microsoft.com"`.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Program.cs" id="HttpClientSnippet":::

1. <span data-ttu-id="e6ea5-142">Ajoutez le code suivant avant la `await builder.Build().RunAsync();` ligne.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-142">Add the following code before the `await builder.Build().RunAsync();` line.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Program.cs" id="AddGraphClientFactorySnippet":::

    <span data-ttu-id="e6ea5-143">Cela ajoute le **GraphClientFactory** en tant que service étendu que nous pouvons mettre à disposition via l’injection de dépendance.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-143">This adds the **GraphClientFactory** as a scoped service that we can make available via dependency injection.</span></span>

1. <span data-ttu-id="e6ea5-144">Ouvrez **./Graph/GraphUserAccountFactory.cs** et ajoutez la propriété suivante à la classe.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-144">Open **./Graph/GraphUserAccountFactory.cs** and add the following property to the class.</span></span>

    ```csharp
    private readonly GraphClientFactory clientFactory;
    ```

1. <span data-ttu-id="e6ea5-145">Mettez à jour le constructeur pour qu’il prenne un paramètre **GraphClientFactory** et affectez-le à la `clientFactory` propriété.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-145">Update the constructor to take a **GraphClientFactory** parameter and assign it to the `clientFactory` property.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/GraphUserAccountFactory.cs" id="ConstructorSnippet" highlight="2,7":::

1. <span data-ttu-id="e6ea5-146">Remplacez la fonction `AddGraphInfoToClaims` existante par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-146">Replace the existing `AddGraphInfoToClaims` function with the following.</span></span>

    :::code language="csharp" source="../demo/GraphTutorial/Graph/GraphUserAccountFactory.cs" id="AddGraphInfoToClaimsSnippet":::

    <span data-ttu-id="e6ea5-147">Examinez ce que fait ce code.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-147">Consider what this code does.</span></span>

    - <span data-ttu-id="e6ea5-148">Il [obtient le profil de l’utilisateur](https://docs.microsoft.com/graph/api/user-get).</span><span class="sxs-lookup"><span data-stu-id="e6ea5-148">It [gets the user's profile](https://docs.microsoft.com/graph/api/user-get).</span></span>
        - <span data-ttu-id="e6ea5-149">Il utilise `Select` pour limiter les propriétés renvoyées.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-149">It uses `Select` to limit which properties are returned.</span></span>
    - <span data-ttu-id="e6ea5-150">Il [obtient la photo de l’utilisateur](https://docs.microsoft.com/graph/api/profilephoto-get).</span><span class="sxs-lookup"><span data-stu-id="e6ea5-150">It [gets the user's photo](https://docs.microsoft.com/graph/api/profilephoto-get).</span></span>
        - <span data-ttu-id="e6ea5-151">Il demande spécifiquement la version en pixels 48 x 48 de la photo de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-151">It requests specifically the 48x48 pixel version of the user's photo.</span></span>
    - <span data-ttu-id="e6ea5-152">Il ajoute les informations au **ClaimsPrincipal**.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-152">It adds the information to the **ClaimsPrincipal**.</span></span>

1. <span data-ttu-id="e6ea5-153">Ouvrez **./Shared/LoginDisplay.Razor** et effectuez les modifications suivantes.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-153">Open **./Shared/LoginDisplay.razor** and make the following changes.</span></span>

    - <span data-ttu-id="e6ea5-154">Remplacez `/img/no-profile-photo.png` par `@(context.User.GetUserGraphPhoto() ?? "/img/no-profile-photo.png")` .</span><span class="sxs-lookup"><span data-stu-id="e6ea5-154">Replace `/img/no-profile-photo.png` with `@(context.User.GetUserGraphPhoto() ?? "/img/no-profile-photo.png")`.</span></span>
    - <span data-ttu-id="e6ea5-155">Remplacez `placeholder@contoso.com` par `@context.User.GetUserGraphEmail()` .</span><span class="sxs-lookup"><span data-stu-id="e6ea5-155">Replace `placeholder@contoso.com` with `@context.User.GetUserGraphEmail()`.</span></span>

    ```razor
    ...
    <img src="@(context.User.GetUserGraphPhoto() ?? "/img/no-profile-photo.png")"
         class="nav-profile-photo rounded-circle align-self-center mr-2">

    ...

    <p class="dropdown-item-text text-muted mb-0">@context.User.GetUserGraphEmail()</p>
    ...
    ```

1. <span data-ttu-id="e6ea5-156">Enregistrez toutes vos modifications et redémarrez l’application.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-156">Save all of your changes and restart the app.</span></span> <span data-ttu-id="e6ea5-157">Connectez-vous à l’application.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-157">Log into the app.</span></span> <span data-ttu-id="e6ea5-158">L’application se met à jour pour afficher la photo de l’utilisateur dans le menu supérieur.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-158">The app updates to show the user's photo in the top menu.</span></span> <span data-ttu-id="e6ea5-159">La sélection de la photo de l’utilisateur ouvre un menu déroulant avec le nom, l’adresse de messagerie et le bouton de **déconnexion** de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e6ea5-159">Selecting the user's photo opens a drop-down menu with the user's name, email address, and a **Log out** button.</span></span>

    ![Capture d’écran de l’application avec la photo de l’utilisateur affichée](images/user-photo.png)

    ![Capture d’écran du menu déroulant](images/user-info.png)
