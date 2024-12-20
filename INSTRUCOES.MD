## TUTORIAL COMO REALIZAR DEPLOY DE CONTRATOS INTELIGENTES UTILIZANDO FOUNDRY (In English file INSTRUCTIONS.MD)

Este repositório tem como objetivo demonstrar como realizar deploy de contratos inteligentes utilizando foundry. 

Foundry é uma ferramenta utilizada para desenvolvimento, teste e avaliação de seguranção de contratos inteligentes. O software
possui uma gama de recursos que facilitam o pipeline de desenvolvimento até os estágios finais, por estes motivos vem 
ganhando adoção na comunidade que desenvolve, testa e realiza auditoria de contratos inteligentes. 

Neste repositório é apresentado passo a passo de configuração do Foundry para deploy de contratos de IDD da comunidade open source
de VDR.

Nota: Algumas etapas não serão descritas, pois já existe documentação em bom nível a respeito, nestes casos será direcionado
para a URL da documentação na seção.

### 1.Instalação do Foundry 

Executar o comando: ``` SHELL curl -L https://foundry.paradigm.xyz | bash ```

Em seguida: ``` SHELL foundryup ```

Nota: Este primeiro passo é útil para quem não possui o Foundry instalado. Se já tem a ferramenta, pule para o passo 2.

### 2.Configuração do Foundry

É recomendado primeiramente inicializar o Foundry com um novo projeto para em seguida copiar os arquivos dos contratos. 

2.1 #### Iniciar novo projeto foundry

 Insira o comando: ``` forge init <nome-do-projeto> ``` 

2.2 #### Forge Build

Este comando realiza as primeiras configurações como donwload de dependencias do foundry para que os comandos forge sejam executados

Insira o comando: ``` forge build ``` 

### 3. Copiando ou criando os arquivos dos contratos

Agora que o foundry deve está funcionando corretamente

Os contratos inteligentes devem ser copiados ou criados na pasta ```src``` do foundry. É recomendado criar uma subpasta
``` contracts ```, desta forma: ``` src/contracts ```


### 4. Importando bibliotecas 

#### 4.1 Teste de dependência
Com os contratos na pasta correta, agora execute o comando: 
``` forge test ```

Este comando realiza testes nos contratos, porém se as dependencias não tiverem sido importadas previamente o comando mostrará
as bibliotecas de código (p.ex: openzeppelin) que necessitam ser instaladas. O comando é um bom mecanismo para encontrar erros antes de tentar realizar deploy.

#### 4.2 Instalando dependências de código (Bibliotecas).

Para instalar as dependências dos contratos basta utilizar o comando ``` forge install <nome-dependencia>```

No caso do openzeppelin basta executar o comando: ``` forge install OpenZeppelin/openzeppelin-contracts ```


#### 4.3 Configurando Remappings
Foundry possui um recurso que permite utilizar alias no import de dependências dos contratos (p.ex: openzeppelin). 

Ao invés de importar bibliotcas nos contratos utilizando o caminho todo como: ``` lib/openzeppelin-contracts ```
é possível utilizar o alias nos imports: ``` @openzeppelin=lib/openzeppelin-contracts/ ``` 

para utilizar o recurso, crie um arquivo na raiz chamado ``` remappings.txt ``` e preencha o arquivo, como no exemplo: 

``` @openzeppelin=lib/openzeppelin-contracts/ ```
``` @dk1a=lib/solidity-stringutils/ ```


Utilizar o Alias pode ser útil por que alguns contratos realizam imports utilizando o padrão ``` @<nome-dependencia> ```
e ajustar todos os imports seria muito trabalhoso. Mas ajustar o alias com remappings resolve o problema.


### Script de Deploy