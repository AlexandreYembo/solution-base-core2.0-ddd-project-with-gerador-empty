# seed-core-ddd-project-with-gerador-empty
Seed vazio para projetos  SPA / DDD / Gerador

1-) Clonar Esse Rep na pasta C:\Projetos (git clone https://github.com/wilsonsantosnet/solution-base-core2.0-ddd-project-with-gerador-empty.git)

1.1 -) Crie um banco de dados com o script da pasta \Projetos\seed-core-ddd-project-with-gerador-empty\Gerador.Gen\Scripts\Sample.Seed.sql

2-) abrir solution seed.sln

3-) compilar projeto

4-) Conferir arquivo ConfigExternalResources no greador para ver quais repositórios serão clonados, e em quais pastas os arquivos serão copiados

5-) Clicar com botão direito no projeto de gerador e rodar em debug

6-) escolher a opção 1 (clonar e copiar para aplicação)

7-) No projeto Greador.Gen Mostar Todos os Arquivos 

8-) Incluir a pasta template no projeto

9-) Selecionar todos os aquivos da pasta Back e Front, clicar com botão direito , opção property e marcar para Copiar Sempre (Copy Always)

10-) Compilar

12-) abrir prompt de comando entrar na pasta Seed.Spa.UI rodar npm install  e logo depois npm rebuild node-sass --force

13-) no gerador configurar a classe ConfigContext com as tabelas que serão geradas [linha 46]

14-) Configurar connection string no gerador app.config apontando para o seu banco. 

15-) Verifica no arquivo App.Config os caminhos onde serão gerador os arquivos de Back e front variaves de appSettings

16-) Rodar gerador opção 3 (gerar código)

17-) no projeto Seed.Api pasta Services configurar a connectionstring do arquivo appsettings.json

18-) No projeto Seed.ui pasta Presentation, encontrar o arquivo /src/app/global.service.ts, nesse arquivo existe uma classe chamanda AuthSettings com uma propriedade chamada CLIENT_ID, essa propriedade deve conter o valor  da propriedade ClientId confirada no item do tipo implicit, no método GetClients do arquivo Config.cs do projeto de Sso.Server.Api da pata SSO\Auth 

19-) No projeto de Seed.API da pasta Services no arquivo  Program descomentar  essa linha ".UseStartup<Startup>()"

20-) No projeto de Sso.Server.Api da pata SSO\Auth no arquivo UserServices descomentar código de autenticação defualt e retira o throw

21-) No projeto de Sso.Server.Api da pata SSO\Auth no arquivo Startup.cs na linha AddIdentityServer , remover o ponto e virgula e descomentar as linhas baixo

22-) o método AddSigningCredential carrega um certificadigital auto assinado contido na pasta pfx, verifique se esse aquivo existe, ou utilize um certificado  que desejar.

23-) Clicar com botão direito na Solution , item propertys, startup Project , escolher Multiple Startup Project e marcar como start os projetos de Seed.Api / Sso.Server.Api

24-) entra na pasta Seed.Spa.Ui e rodar no prompt de comando ng serve --open

25-) agora pode criar outros campos na Tabela Rodar o gerador que esses serão criados em cada camada do projeto, inclusive no front

https://drive.google.com/file/d/1qE6RSNoJCipIbQMYFmT41_Y7GXW2WXds/view

# EXEMPLO CONFIG.CONTEXT 
## 1-) CRUD com customização de Campos
## 2-) CRUD 
## 3-) Component Basico sem back 

```
  private Context ConfigContextDefault()
        {
            var contextName = "Seed";

            return new Context
            {

                ConnectionString = ConfigurationManager.ConnectionStrings["Seed"].ConnectionString,

                Namespace = "Seed",
                ContextName = contextName,
                ShowKeysInFront = false,
                LengthBigField = 250,
                OverrideFiles = true,
                UseRouteGuardInFront = true,

                OutputClassDomain = ConfigurationManager.AppSettings[string.Format("outputClassDomain")],
                OutputClassInfra = ConfigurationManager.AppSettings[string.Format("outputClassInfra")],
                OutputClassDto = ConfigurationManager.AppSettings[string.Format("outputClassDto")],
                OutputClassApp = ConfigurationManager.AppSettings[string.Format("outputClassApp")],
                OutputClassApi = ConfigurationManager.AppSettings[string.Format("outputClassApi")],
                OutputClassFilter = ConfigurationManager.AppSettings[string.Format("outputClassFilter")],
                OutputClassSummary = ConfigurationManager.AppSettings[string.Format("outputClassSummary")],
                OutputAngular = ConfigurationManager.AppSettings["OutputAngular"],
                OutputClassSso = ConfigurationManager.AppSettings["OutputClassSso"],
                OutputClassCrossCustingAuth = ConfigurationManager.AppSettings["OutputClassCrossCustingAuth"],

                Arquiteture = ArquitetureType.DDD,
                CamelCasing = true,
                MakeFront = true,
                AlertNotFoundTable = true,
                MakeToolsProfile = true,

                Routes = new List<RouteConfig> {
                    new RouteConfig{ Route = "{ path: 'sampledash',  canActivate: [AuthGuard], loadChildren: './main/sampledash/sampledash.module#SampleDashModule' }" }
                },
                
                TableInfo = new UniqueListTableInfo
                {
                   new TableInfo().FromTable("Sample").MakeBack().MakeFront().AndConfigureThisFields(new List<FieldConfig> {
                       new FieldConfig
                       {
                           Name = "Valor",
                           Attributes = new List<string>{ "[textMask]='{mask: vm.masks.maskMoney}'" }
                       }
                   }),
                   new TableInfo().FromTable("SampleType").MakeBack().MakeFront(),
                   new TableInfo().FromClass("SampleDash").MakeFrontBasic(),
                }
            };
        }
```

-- PRÉ REQUISITOS;

1-) git shell [https://git-for-windows.github.io/]

2-) node.js [https://nodejs.org/en/])

3-) npm install -g @angular/cli

3-) opcional [Conemu [https://www.fosshub.com/ConEmu.html/ConEmuSetup.161206.exe]]

5-) instalar .net core 2.0.X [https://www.microsoft.com/net/download/windows]

5.1-) instalar SDK installer [https://www.microsoft.com/net/download/thank-you/dotnet-sdk-2.1.200-windows-x64-installer]



