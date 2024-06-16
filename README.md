# Desafio Dio - Entendendo sobre Segurança e Identidade na Azure



####     Projeto ainda mais completo e abrangente com mais códigos para: Entendendo sobre Segurança e Identidade na Azure



**Introdução**

Este projeto irá guiá-lo pelos fundamentos de segurança e identidade no Microsoft Azure, uma plataforma de computação em nuvem que oferece uma ampla gama de serviços para ajudá-lo a construir, implantar e gerenciar seus aplicativos com segurança.



### **Pré-requisitos**

- Uma conta do Microsoft Azure

- O Visual Studio 2019 ou superior

- O .NET Core SDK 3.1 ou superior

  

### **Instruções**

1. **Crie um novo projeto do Visual Studio.**

2. **Selecione o modelo "Aplicativo Web do ASP.NET Core".**

3. **Nomeie o projeto como "AzureSecurityAndIdentityInAction".**

4. **Clique em "Criar".**

   

5. #### Adicione os seguintes pacotes NuGet ao projeto:

   

   - Microsoft.Azure.Management.KeyVault

   - Microsoft.Azure.Management.Storage

   - Microsoft.Azure.Storage.Blob

   - Microsoft.Azure.ActiveDirectory.GraphClient

   - Microsoft.IdentityModel.Clients.ActiveDirectory

     

6. #### Adicione as seguintes classes ao projeto:

   

   - **KeyVaultService.cs:** Esta classe fornece métodos para interagir com o serviço de cofre de chaves do Azure.

   - **StorageService.cs:** Esta classe fornece métodos para interagir com o serviço de armazenamento do Azure.

   - **BlobStorageService.cs:** Esta classe fornece métodos para interagir com o serviço de armazenamento de blobs do Azure.

   - **ActiveDirectoryService.cs:** Esta classe fornece métodos para interagir com o serviço Active Directory do Azure.

     

7. #### **Adicione o seguinte código ao arquivo "Startup.cs":**

   

csharp



```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IKeyVaultService, KeyVaultService>();
    services.AddSingleton<IStorageService, StorageService>();
    services.AddSingleton<IBlobStorageService, BlobStorageService>();
    services.AddSingleton<IActiveDirectoryService, ActiveDirectoryService>();
}
```



1. #### **Adicione o seguinte código ao arquivo "Controllers/HomeController.cs":**

   

csharp



```csharp
public class HomeController : Controller
{
    private readonly IKeyVaultService _keyVaultService;
    private readonly IStorageService _storageService;
    private readonly IBlobStorageService _blobStorageService;
    private readonly IActiveDirectoryService _activeDirectoryService;

    public HomeController(IKeyVaultService keyVaultService, IStorageService storageService, IBlobStorageService blobStorageService, IActiveDirectoryService activeDirectoryService)
    {
        _keyVaultService = keyVaultService;
        _storageService = storageService;
        _blobStorageService = blobStorageService;
        _activeDirectoryService = activeDirectoryService;
    }

    public IActionResult Index()
    {
        return View();
    }

    [HttpPost]
    public async Task<IActionResult> CreateKeyVault(string name)
    {
        await _keyVaultService.CreateKeyVaultAsync(name);

        return RedirectToAction("Index");
    }

    [HttpPost]
    public async Task<IActionResult> CreateStorageAccount(string name)
    {
        await _storageService.CreateStorageAccountAsync(name);

        return RedirectToAction("Index");
    }

    [HttpPost]
    public async Task<IActionResult> UploadFile(IFormFile file)
    {
        await _blobStorageService.UploadBlobAsync(file.FileName, file.OpenReadStream());

        return RedirectToAction("Index");
    }

    [HttpPost]
    public async Task<IActionResult> CreateUser(string name, string password)
    {
        await _activeDirectoryService.CreateUserAsync(name, password);

        return RedirectToAction("Index");
    }
}
```



1. #### **Execute o projeto.**

   

## **Conclusão**



Este projeto fornece uma base ainda mais sólida para você começar a construir segurança e identidade na nuvem no Microsoft Azure. Você pode usar os serviços de cofre de chaves, armazenamento, armazenamento de blobs e Active Directory para criar e gerenciar cofres de chaves, contas de armazenamento, blobs de armazenamento e usuários do Active Directory.



