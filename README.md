# Desafio DIO - AWS CloudFormation

## Descrição do Desafio

Este laboratório tem como objetivo implementar uma infraestrutura automatizada utilizando **AWS CloudFormation**. O entregável consiste em um repositório organizado contendo anotações, prints simulados, templates e insights adquiridos durante a prática.

## Objetivos de Aprendizagem

- Aplicar conceitos aprendidos em um ambiente prático;
- Documentar processos técnicos de forma clara e estruturada;
- Utilizar o GitHub como ferramenta para compartilhamento de documentação técnica.

## Estrutura do Repositório

- **templates/**: Contém os arquivos YAML/JSON do CloudFormation.
- **images/**: Capturas de tela da execução e resultados.
- **docs/**: Documentação detalhada do passo a passo e insights.
- **README.md**: Este arquivo de apresentação.

## Passo a Passo

1. Criação da VPC
2. Criação de Security Group
3. Criação de EC2
4. Verificação do status da stack
5. Documentação de prints e insights

> Exemplo de print do status da stack:  
> ![Stack Event](images/stack_event.png)

## Arquivo de Template

O template `myfirststack.yaml` contém os recursos básicos:

```yaml
AWSTemplateFormatVersion: "2010-09-09"
Description: "Stack simples - EC2 + Security Group + VPC"

Resources:
  MyVPC:
    Type: "AWS::EC2::VPC"
    Properties:
      CidrBlock: "10.0.0.0/16"
      EnableDnsSupport: true
      EnableDnsHostnames: true
      Tags:
        - Key: Name
          Value: "MyVPC"

  MySecurityGroup:
    Type: "AWS::EC2::SecurityGroup"
    Properties:
      GroupDescription: "Security Group para EC2"
      VpcId: !Ref MyVPC
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0

  MyInstance:
    Type: "AWS::EC2::Instance"
    Properties:
      ImageId: "ami-051f8a213df8bc089"
      InstanceType: "t2.micro"
      SecurityGroupIds:
        - !Ref MySecurityGroup
      SubnetId: !Ref MyVPC
