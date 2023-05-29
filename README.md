# Adding security to APIs using Amazon Cognito


## 🛠 LAB

criar uma API como o Amazon API Gateway
criar uma tabela de banco de dados com DynamoDB
Criar funcoes de backend com o AWS Lambda
Criar uma User Pool com o Amazon Cognito
Configurar Authorizers para garantir a autenticacao de endpoints da API
Registrar e realizar o login de usuarios
interagir com a aplicao criada


figura cognito-arquitetura - see aws folder



management console
search api 
select api gateway
select REST API
select New API
inform name and select regional
select Create API

Recurso e o q vem depois do dominio

create resource itens



Explicar CORS


criar Dynamo DB table

management console
Search dynamoDB
create table items

search key id
partitionkey


LAB - marcar peres-assiano
cassianobrexit


criar funcao lambda

search lambda
select lambda
create a function
author from scrat
dio_lambda_function
select create function


agora vamos trabalhar com o IAM
A funcao lambda vai falar com a tabela do BD precisa de permissao para acessar a tabela

```javascript
export const handler = async(event) => {
    // TODO implement
    const response = {
        statusCode: 200,
        body: JSON.stringify('Hello from Lambda!'),
    };
    return response;
};

```
nova funcao
```javascript


/*import needed libraries*/
var AWS = require("aws-sdk");
const dynamodb = new AWS.DynamoDB.DocumentClient();


exports.handler = async(event) => {
    
    let responseBody = ""
    let statusCode = 0
    
    let {id, price} = JSON.parse(event.body);
    
    
    /*define the parameters*/
    const params = {
        TableName: "itens",
        Item: {
            id : id,
            price : price
        }
    }
    
    try{
        /*call the dyanmoDb put method*/
        await dynamodb.put(params).promise();
        statusCode = 200,
        responseBody = JSON.stringify("item inserted");
    }catch (err){
        statusCode = 200,
        stringify = JSON.stringify(err);
    }
    
    const response = {
        statusCode: statusCode,
        body: responseBody,        
    };    
    return response;
};


```

o novo codigo 



import { DynamoDBClient } from "@aws-sdk/client-dynamodb";
import {
  DynamoDBDocumentClient,
  ScanCommand,
  PutCommand,
  GetCommand,
  DeleteCommand,
} from "@aws-sdk/lib-dynamodb";


const client = new DynamoDBClient({});

const dynamo = DynamoDBDocumentClient.from(client);

export const handler = async(event) => {
    
    let responseBody = ""
    let statusCode = 0
    
    let {id, price} = JSON.parse(event.body);
    
    
    /*define the parameters*/
    const params = {
        TableName: "itens",
        Item: {
            id : id,
            price : price
        }
    }
    
    try{
        /*call the dyanmoDb put method*/
        await dynamodb.put(params).promise();
        statusCode = 200,
        responseBody = JSON.stringify("item inserted");
    }catch (err){
        statusCode = 200,
        stringify = JSON.stringify(err);
    }
    
    const response = {
        statusCode: statusCode,
        body: responseBody,        
    };    
    return response;
};



Agora vamos definir as permissoes de acesso

Configuraiton > permissions > Execution role
open role name dio_lambda_function-role-mhoroobq 

devemos adicionar uma nova politica na role

add inline police
type DynamoDB
Add actions => putItem nao da para criar pois o botao addaction esta desabilitado

Entao eu vou apenas selecionar Write > putitem

Adcionar o ARN do objeto
voltar na tabela do dynamoDB 
overview > aditional info

dar  o nome da politica de acesso putitem_policy
create policy


escrever dados dentro do dynamoDB

1 - Integrar api gateway com backend lambda para 
Amazon API Gatewy > dio_live_api > Resources > Action > Create Method > Select Post


Inform lambda fucntion : dio_lambda_function

![screen 1](/assets/images/api_gateway_post_method.png)
para gerar um endpoint devemos publicar a nossa Api
Actions > Deploy API
new Stage Development


![screen 1](/assets/images/api_gateway_post_method_flow.png)


Get the url at > Stages > Development > items > POST



Agora vamos testar com o postman:

Select Post
Use the api url defined before
Set up the body > Raw > Json

```javascript

{
    "id":"003",
    "price" : 800
}
```


