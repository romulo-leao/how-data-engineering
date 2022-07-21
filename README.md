# Projeto de Arquitetura para Recursos Humanos / People Analytics
## Sobre:

Este repositório tem como objetivo disponibilizar a arquitetura criada no checkpoint 6 do bootcamp de Engenharia de Dados, da HowBootcamps. O desafio era criar uma arquitetura simples com os conceitos sobre AWS aprendidos durante as 11 semanas do curso. Utilizei o Excalidraw para montar a arquitetura pensando nos desafios que enfrento no meu dia a dia, como Especialista de People Analytics.

## Objetivo:

O objetivo do projeto é criar um pipeline em nuvem dos dados de recrutamento e seleção e de recursos humanos de uma empresa (salarios, promocoes, desligamentos, afastamentos, pontos, etc) e informações vindas dos sistemas de comunicação oficiais da empresa (que funcionam como redes sociais). A centralização dessas informações em um único DL/DW, além de facilitar o trabalho dos analistas no dia a dia, também permite que o time de People Analytics faça analises mais profundas, inclusive fornecendo features robustas para um futuro trabalho de predição de turn-over.

## Descrição do processo

Os dados viriam de 3 APIs: da Kenoby, do Apdata (o sistema de RH) e o Discovery (a ferramenta de comunicação). Os dois primeiros não há necessidades de ingestão por streaming, pela natureza dos dados, então poderiam passar periódicamente pelo Glue, via crawlers, e ali serem catalogados. Já a API do discovery, pela natureza de rede social, seria streamada por SQS e Kinesis e, após isso, seria armazenado na camada bronze/prata em um bucket S3.

Após ETL realizado com o dbt, os dados migrariam para a camada ouro, o Data Warehouse, onde poderiam ser ingeridos diretamente pelo PowerBI, para análises diagnósticas e descritivas, além do Athena, caso os analistas precisem extrair os dados com mais personalização. Por fim, ainda existiria uma integração de mão-dupla com o sagemaker, onde os cientistas de dados da equipe poderiam modelar os dados de predição de turn-over e retroalimentar o sistema.

## Arquitetura:
