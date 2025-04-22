# UploadXMLFDC

Programa Java para leitura e envio automático de XMLs (NFe e CTe) para Oracle Cloud. Compatível com sistemas Windows e Linux. Não requer instalação do Java na máquina.

## 📂 Estrutura do Projeto

- `jre/`  
  Java Runtime Environment incluso — permite executar o programa mesmo sem Java instalado (somente para Windows).

- `lib/`  
  Contém bibliotecas do wrapper necessárias para execução como serviço no Linux.

- `log/`  
  Diretório onde são gerados os logs do sistema. Útil para verificar erros na leitura de XMLs ou na inicialização.

- `resources/`  
  Arquivos de configuração. Inclui `application.properties` com a URL do Oracle, usuário e senha. **Não funciona com autenticação SSO.**

- `UploadXMLFDC.jar`  
  Arquivo principal. Responsável por:
  - Ler os XMLs (NFe e CTe) da pasta configurada.
  - Enviar os dados para Oracle Cloud.
  - Executar dois jobs por XML com base no CNPJ e número extraídos.

- `install.bat`  
  Instala o serviço no Windows.

- `remove.bat`  
  Remove o serviço do Windows (caso necessário, por erro ou manutenção).

- `Start.bat`  
  Inicia o sistema sem precisar instalar como serviço (útil para testes rápidos no Windows).

- `UploadXMLFDC.sh`  
  Script para rodar o programa no Linux.

- `wrapper.exe`  
  Serviço wrapper que lê as configurações em `resources/` para executar o JAR como serviço.

## 🧠 O que o programa faz?

1. Lê os arquivos XML (NFe ou CTe) adicionados na pasta definida em `resources/application.properties`.
2. Move os arquivos processados para a pasta `Lido/`.
3. Extrai o **CNPJ** e o **número** de cada XML.
4. Executa dois **jobs** na Oracle Cloud:
   - Validação do XML
   - Importação para uso posterior

## 💻 Como usar

### Windows

1. **Instalação como serviço:**
   install.bat

2. **Remoção do serviço:**
   remove.bat
   
3. **Execução rápida (sem instalar serviço):**
   Start.bat
   
###Linux
1. **Dê permissão ao script:**
   chmod +x UploadXMLFDC.sh
   
2. **Execute o programa:**	
   ./UploadXMLFDC.sh
   
Obs: Certifique-se de que a pasta lib/ está presente, pois ela é obrigatória para o funcionamento como serviço no Linux.

⚙️ Configuração

No arquivo resources/application.properties, configure:

spring.application.name=UploadXMLFDC
oracle.cloud.url=https://oraclecloud.com
oracle.cloud.username=USUARIO
oracle.cloud.password=SENHA

#Caminho do XML
path.dir.xml=D:/XML/
path.dir.lido=D:/XML/lido/

#Configuração para Download XML SEFAZ
empresa.cnpj=
empresa.uf=
empresa.download=N

#Caminho do Certificado Digital
certificado.dir=
certificado.password=

⚠️ A conexão via SSO não é suportada.


📝 Requisitos

    Pasta de origem dos XMLs deve ser definida no application.properties

    Criar a subpasta Lido/ para arquivos processados

    Ter permissão de execução no sistema operacional

    Oracle Cloud configurado com os jobs esperados

🧑‍💻 Autor

Desenvolvido por Cristiano Silva
Especialista em integração fiscal, Oracle Cloud e automação de processos XML
