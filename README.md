# FIWARE-Lab@RNP - Descrição do Experimento

A atividade proposta no experimento consiste na configuração de um ambiente composto por um conjunto de serviços (GEs) FIWARE, para dar suporte a uma aplicação de sala inteligente.

Alguns dispositivos estão instalados em cada sala e são responsáveis por monitorar variáveis do ambiente como **temperatura**, **umidade**, **se há ocupação**, **número de pessoas**,  bem como **enviar comandos para controle de um aparelho de ar condicionado** instalado em cada sala.

## Configuração de ambiente

Para dar suporte a tal aplicação, é necessário inicialmente configurar o conjunto de serviços FIWARE necessário às funcionalidades da aplicação. São esses serviços:

- Orion Context Broker
- IoT-Agent UltraLight    
- Cygnus

Em adição, para conexão com tais serviços, já são fornecidas algumas instâncias de bancos de dados necessários para cada serviço:

- MongoDB (utilizado pelo Orion Context Broker e IoT-Agent)    
- PostgreSQL (utilizado pelo Cygnus)
    
Os componentes FIWARE necessários para a execução da tarefa podem ser visualizados na imagem abaixo, que apresenta a arquitetura e a forma de conexão desses componentes:

![Arquitetura de componentes FIWARE da aplicação](/images/application-fiware-architecture.png)


## Configuração da aplicação
  
  Uma vez que os serviços se encontrem em execução, para fornecer o suporte à aplicação, os seguintes itens devem ser configurados em seus respectivos componentes:

- Criar serviço para a aplicação

Em seguida, no serviço criado:

- Criar entidade da sala monitorada
- Criar dispositivos (sensores e atuador) associados à sala monitorada
- Criar subscrição para persistência de dados do sensor de temperatura (temp001)

As informações detalhadas dos itens a serem criados são detalhadas na tabela abaixo:

### Serviço
- name: IMDService
- path: /imd
  

### Entidades
    

**urn:ngsi-ld:Room:001**
- ID: urn:ngsi-ld:Room:001
- Type: Room
- Attributes:
	- temperature
	    - Type: Integer
		- Value: 22
		- metadata:
			- precision:
				- Type: Integer
				- Value: 2
	- humidity
		- Type: Float
		- Value: 20.5
		- metadata:
			- precision:
				- Type: Integer
				- Value: 2
	- presence
		- Type: Boolean
		- Value: False
	- numPeople
		- Type: Integer
		- Value: 10

### Devices

**temp001**
- Device ID: temp001
- Entity name: urn:ngsi-ld:Temperature:001
- Entity type: Temperature
- Protocol: PDI-IoTA-UltraLight
- Transport: MQTT
- Attributes:
	- temperature
		- ID: t
		- Name: temperature
		- Type: Integer
- Static attributes:
	- refRoom
		- Name: refRoom
		- Type: Relationship
		- Value: urn:ngsi-ld:Room:001

**hum001**
- Device ID: hum001
- Entity name: urn:ngsi-ld:Humidity:001
- Entity type: Humidity
- Protocol: PDI-IoTA-UltraLight
- Transport: MQTT
- Attributes:
	- humidity
		- ID: h
		- Name: humidity
		- Type: Integer
- Static attributes:
	- refRoom
		- Name: refRoom
		- Type: Relationship
		- Value: urn:ngsi-ld:Room:001

**mot001**
- Device ID: mot001
- Entity name: urn:ngsi-ld:Motion:001
- Entity type: Motion
- Protocol: PDI-IoTA-UltraLight
- Transport: MQTT
- Attributes:
	- motion
		- ID: d
		- Name: detected
		- Type: Boolean
- Static attributes:
	- refRoom
		- Name: refRoom
		- Type: Relationship
		- Value: urn:ngsi-ld:Room:001

**remote001**
- Device ID: remote001
- Entity name: urn:ngsi-ld:Remote:001
- Entity type: Remote
- Protocol: PDI-IoTA-UltraLight
- Transport: MQTT
- Commands:
	- changeState
		- Name: changeState
		- Type: command
- Static attributes:
	- refRoom
		- Name: refRoom
		- Type: Relationship
		- Value: urn:ngsi-ld:Room:001

## Guias e material de apoio

Para a realização das tarefas, a documentação e guias oficiais do FIWARE podem ser consultados. A fim de facilitação, abaixo são listados alguns guias, disponíveis em repositório do Github no FIWARE, que contém instruções relacionadas com as tarefas:

[Step-by-Step Guide](https://github.com/FIWARE/tutorials.Step-by-Step)

[101. Getting Started](https://github.com/FIWARE/tutorials.Getting-Started)
[103. CRUD Operations](https://github.com/FIWARE/tutorials.CRUD-Operations)
[106. Subscribing to Changes in Context](https://github.com/FIWARE/tutorials.Subscriptions)

[201. Introduction to IoT Sensors](https://github.com/FIWARE/tutorials.IoT-Sensors)
[202. Provisioning an IoT Agent](https://github.com/FIWARE/tutorials.IoT-Agent)
[203. IoT over MQTT](https://github.com/FIWARE/tutorials.IoT-over-MQTT)

[301. Persisting Context Data using Apache Flume (MongoDB, MySQL, PostgreSQL](https://github.com/FIWARE/tutorials.Historic-Context-Flume)

## Formulário Final

Ao final da realização das atividades, favor responder o link em anexo para finalização da participação no experimento:

[Link do formulário do experimento](https://forms.gle/Ue8zNDk7XPC98Gxu9)
