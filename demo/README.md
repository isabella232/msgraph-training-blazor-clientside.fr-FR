---
ms.openlocfilehash: 9029486df6b08042681c0a1a67b156cbbd0381a0
ms.sourcegitcommit: 5067c508675fbedbc7eead0869308d00b63be8e3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2020
ms.locfileid: "49584607"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="5d7e4-101">Exécution du projet terminé</span><span class="sxs-lookup"><span data-stu-id="5d7e4-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d7e4-102">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="5d7e4-102">Prerequisites</span></span>

<span data-ttu-id="5d7e4-103">Pour exécuter le projet terminé dans ce dossier, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5d7e4-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="5d7e4-104">Le [Kit de développement logiciel .net Core](https://dotnet.microsoft.com/download) installé sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-104">The [.NET Core SDK](https://dotnet.microsoft.com/download) installed on your development machine.</span></span> <span data-ttu-id="5d7e4-105">(**Remarque :** ce didacticiel a été écrit avec .net Core SDK version 3.1.402.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-105">(**Note:** This tutorial was written with .NET Core SDK version 3.1.402.</span></span> <span data-ttu-id="5d7e4-106">Les étapes de ce guide peuvent fonctionner avec d’autres versions, mais cela n’a pas été testé.)</span><span class="sxs-lookup"><span data-stu-id="5d7e4-106">The steps in this guide may work with other versions, but that has not been tested.)</span></span>
- <span data-ttu-id="5d7e4-107">Soit un compte Microsoft personnel avec une boîte aux lettres sur Outlook.com, soit un compte professionnel ou scolaire Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-107">Either a personal Microsoft account with a mailbox on Outlook.com, or a Microsoft work or school account.</span></span>

<span data-ttu-id="5d7e4-108">Si vous n’avez pas de compte Microsoft, vous disposez de deux options pour obtenir un compte gratuit :</span><span class="sxs-lookup"><span data-stu-id="5d7e4-108">If you don't have a Microsoft account, there are a couple of options to get a free account:</span></span>

- <span data-ttu-id="5d7e4-109">Vous pouvez vous [inscrire pour obtenir un nouveau compte Microsoft personnel](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span><span class="sxs-lookup"><span data-stu-id="5d7e4-109">You can [sign up for a new personal Microsoft account](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).</span></span>
- <span data-ttu-id="5d7e4-110">Vous pouvez vous [inscrire au programme pour les développeurs office 365](https://developer.microsoft.com/office/dev-program) pour obtenir un abonnement gratuit à Office 365.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-110">You can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

## <a name="register-a-web-application-with-the-azure-active-directory-admin-center"></a><span data-ttu-id="5d7e4-111">Enregistrer une application Web avec le centre d’administration Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d7e4-111">Register a web application with the Azure Active Directory admin center</span></span>

1. <span data-ttu-id="5d7e4-112">Ouvrez un navigateur et accédez au [Centre d’administration Azure Active Directory](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5d7e4-112">Open a browser and navigate to the [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="5d7e4-113">Connectez-vous à l’aide d’un **compte personnel** (compte Microsoft) ou d’un **compte professionnel ou scolaire**.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-113">Login using a **personal account** (aka: Microsoft Account) or **Work or School Account**.</span></span>

1. <span data-ttu-id="5d7e4-114">Sélectionnez **Azure Active Directory** dans le volet de navigation gauche, puis sélectionnez **Inscriptions d’applications** sous **Gérer**.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-114">Select **Azure Active Directory** in the left-hand navigation, then select **App registrations** under **Manage**.</span></span>

    ![<span data-ttu-id="5d7e4-115">Une capture d’écran des inscriptions d’applications</span><span class="sxs-lookup"><span data-stu-id="5d7e4-115">A screenshot of the App registrations</span></span> ](../tutorial/images/aad-portal-app-registrations.png)

1. <span data-ttu-id="5d7e4-116">Sélectionnez **Nouvelle inscription**.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-116">Select **New registration**.</span></span> <span data-ttu-id="5d7e4-117">Sur la page **Inscrire une application**, définissez les valeurs comme suit.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-117">On the **Register an application** page, set the values as follows.</span></span>

    - <span data-ttu-id="5d7e4-118">Définissez le **Nom** sur `Blazor Graph Tutorial`.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-118">Set **Name** to `Blazor Graph Tutorial`.</span></span>
    - <span data-ttu-id="5d7e4-119">Définissez les **Types de comptes pris en charge** sur **Comptes dans un annuaire organisationnel et comptes personnels Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-119">Set **Supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**.</span></span>
    - <span data-ttu-id="5d7e4-120">Sous **URI de redirection**, définissez la première flèche déroulante sur `Web`, et la valeur sur `https://localhost:5001/authentication/login-callback`.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-120">Under **Redirect URI**, set the first drop-down to `Web` and set the value to `https://localhost:5001/authentication/login-callback`.</span></span>

    ![Capture d’écran de la page Inscrire une application](../tutorial/images/aad-register-an-app.png)

1. <span data-ttu-id="5d7e4-122">Sélectionner **Inscription**.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-122">Select **Register**.</span></span> <span data-ttu-id="5d7e4-123">Sur la page du **didacticiel de graphique éblouissant** , copiez la valeur de l' **ID d’application (client)** et enregistrez-la, vous en aurez besoin à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-123">On the **Blazor Graph Tutorial** page, copy the value of the **Application (client) ID** and save it, you will need it in the next step.</span></span>

    ![Une capture d’écran de l’ID d’application de la nouvelle inscription d'application](../tutorial/images/aad-application-id.png)

1. <span data-ttu-id="5d7e4-125">Sous **Gérer**, sélectionnez **Authentification**.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-125">Select **Authentication** under **Manage**.</span></span> <span data-ttu-id="5d7e4-126">Recherchez la section **Grant implicite** et activez les **jetons d’accès** et les **jetons ID**.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-126">Locate the **Implicit grant** section and enable **Access tokens** and **ID tokens**.</span></span> <span data-ttu-id="5d7e4-127">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-127">Select **Save**.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="5d7e4-128">Configurer l’exemple</span><span class="sxs-lookup"><span data-stu-id="5d7e4-128">Configure the sample</span></span>

1. <span data-ttu-id="5d7e4-129">Renommez le fichier **/GraphTutorial/wwwroot/appsettings.example.jssur** **appsettings.js**.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-129">Rename the **/GraphTutorial/wwwroot/appsettings.example.json** file to **appsettings.json**.</span></span>

1. <span data-ttu-id="5d7e4-130">Modifiez **appsettings.js** et remplacez `YOUR_APP_ID_HERE` par votre ID d’application.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-130">Edit **appsettings.json** and replace `YOUR_APP_ID_HERE` with your application ID.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="5d7e4-131">Exécution de l’exemple</span><span class="sxs-lookup"><span data-stu-id="5d7e4-131">Run the sample</span></span>

<span data-ttu-id="5d7e4-132">Dans votre interface CLI, exécutez la commande suivante pour démarrer l’application.</span><span class="sxs-lookup"><span data-stu-id="5d7e4-132">In your CLI, run the following command to start the application.</span></span>

```Shell
dotnet run
```
