
## 👋 O Amazon Cognito

Amazon Cognito is a managed service lets you easily add user sign-up and authentication to your mobile and web apps. Amazon Cognito also enables you to authenticate users through an external identity provider and provides temporary security credentials to access your app's backend resources in AWS or any service behind Amazon API Gateway. 
[aws](https://aws.amazon.com/cognito/faqs/#:~:text=Amazon%20Cognito%20lets%20you%20easily,service%20behind%20Amazon%20API%20Gateway)


fornece autenticacao, autorizacao, gerenciamento e sincronizacao de usuarios para aplicacoes web e moveis. Os usuarios podem fazer login diretamente como um nome de usuario e uma senha ou por meio de terceiros, como Facebook, Amazon, Google ou Apple.


principais recuros:

user pools: sao diretorios de usuarios para login em aplicacoes web ou mobile com o Amazon Cognito ou por um provedor de identidades de terceiros (IdP)

identity pools:
permite aos usuarios obter credenciais termporarias da AWS (IAM) para acessar servicos da AWS, como Amazon S3 e o Dynamo DB. Oferece suporte a usuarios convidados anonimos e autenticados.


Beneficios
seguranca aumentada
consistencia entre as plataformas
usuarios anonimos e login social
MFA e politicas de senhas
analise de comportamento de usuarios - cloud watch e cloud trail

pricing
nivel gratuitos de 50.000 MAU's (usuarios ativos mensais) para usuarios que fazem login diretamente no Cognito User Pool e 50 MAU's para usuarios federados por meio de provedores de identidade baseados em SAML 2.0

