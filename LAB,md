
<p align="center">
  <a href="#HowToUseThisProject">How To</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#Lab">Lab</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#memo-license">License</a>
</p>

![Architecture](/assets/images/lab_architecture.png)

### CREATE AN API
[] management console
[] search api 
[] select api gateway
[] select REST API
[] select New API
[] inform name and select regional
[] select Create API</p>
[] create resource itens
</p>



*Recurso e o q vem depois do dominio
*Explicar CORS


### CREATE A DYNAMODB TABLE
[] management console</p>
Search dynamoDB</p>
create table items</p>
search key id</p>
partitionkey</p>


### CREATE A LAMBDA FUNCTION
[] search lambda</p>
[] select lambda</p>
[] create a function</p>
[] author from scrat</p>
[] name: dio_lambda_function</p>
[] select create function</p>

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


```javascript
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

```

### SETTING UP THE PERMISSIONS

agora vamos trabalhar com o IAM
A funcao lambda vai falar com a tabela do BD precisa de permissao para acessar a tabela

[] Configuraiton > permissions > Execution role
[] open role name
[] name dio_lambda_function-role-mhoroobq 

[] add inline police
[] type DynamoDB
[] Add actions => putItem nao da para criar pois o botao addaction esta desabilitado
[] Entao eu vou apenas selecionar Write > putitem
[] Adcionar o ARN do objeto
voltar na tabela do dynamoDB 
overview > aditional info
[] dar  o nome da politica de acesso putitem_policy
create policy

### CREATING THE INTEGRATION AND WRITING THE DATA

[] Integrar api gateway com backend lambda para 
Amazon API Gatewy > dio_live_api > Resources > Action > Create Method > Select Post</p>

[] Inform lambda fucntion : dio_lambda_function</p>

![screen 1](/assets/images/api_gateway_post_method.png)

[] para gerar um endpoint devemos publicar a nossa Api
Actions > Deploy API
new Stage Development</p>


![screen 1](/assets/images/api_gateway_post_method_flow.png)


[] Get the url at > Stages > Development > items > POST</p>



### VALIDATION USING POSTMAN

[] Select Post</p>
[] Use the api url defined before</p>
[]Set up the body > Raw > Json

```javascript 
{
    "id":"003",
    "price" : 800
}
```

![Postman](/assets/images/api_gateway_post_method_postman_success.png)

