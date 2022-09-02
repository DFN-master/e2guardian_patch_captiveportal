# e2guardian_patch_captiveportal
Patch para permitir o Proxy E2Guardian identificar o usuário através da autenticação do Captive Portal no pfSense

## Instalação:

!! Importante: Este procedimento foi homologado para pfSense CE na versão 2.6  
Última atualização: 01/09/2022

### Etapas:  
1- Ajustar hostname e nome de domínio do firewall de acordo com o seu ambiente:  
1.1- A configuração é feita pelo menu System -> General Setup.  

2- Criar o arquivo de configuração externa do serviço DNS:  
2.1- Criar o arquivo /var/unbound/dnsauth.conf vazio com o comando abaixo (executar através do menu Diagnostics -> Command Prompt):  
```
echo> /var/unbound/dnsauth.conf
```
3- Configure o serviço de DNS do pfSense para incluir o arquivo dnsauth.conf.  
3.1- Acesse o menu Services -> DNS Resolver. Clique em Display Custom Options ao final da página e inclua a linha seguinte no campo de texto:  
```
include: /var/unbound/dnsauth.conf
```
4- Realize a instalação do E2Guardian:  
4.1- Vá no menu System -> Package Manager -> Available Packages e instale o pacote System_Patches.  
4.2- Acesse a página abaixo e copie todo o código:  
```
https://raw.githubusercontent.com/marcelloc/Unofficial-pfSense-packages/master/25_unofficial_packages_list.patch
```  
4.3- Acesse o menu System -> Patches. Clique em Add New Patch.  
4.4- Cole o código no campo Patch Contents.  
4.5- Em Description preencha com: Unnoficial_packages.  
4.6- No campo Path Strip Count defina com valor 1 e salve o patch (botão save ao final da página).  
4.7- Clique em apply no patch recem registrado.  
4.8- No menu Diagnostics -> Command Prompt execute o comando abaixo:  
```
fetch -q -o /usr/local/etc/pkg/repos/Unofficial.conf 
https://raw.githubusercontent.com/marcelloc/Unofficial-pfSense-packages/master/Unofficial_25.conf
```
4.9- Ainda no menu Diagnostics -> Command Prompt execute o comando abaixo:
```
pkg update
```
4.10- Acesse o menu System -> Package Manager -> Available Packages e instale o pacote E2Guardian.

5- Realize a configuração do captive portal (adicione uma zona ao captive portal).  
5.1- Acesse Zones -> Captive Portal e clique em Add.  
5.2- Dê um nome e uma descrição para a zona e clique em Add & Continue.  
5.3- Clique em Enable, selecione a interface (LAN).  
5.4- No campo Authentication Server selecione Local database.  
5.5- Clique em Save ao final da página.  

6. 





