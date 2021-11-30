# Teste de Força Bruta com Burp Suite

# 🏁 Indice

- [Sobre](#-sobre)
- [Features](#-features)
- [Tecnologias Utilizadas](#%EF%B8%8F-tecnologias-utilizadas)
- [Como executar o projeto django](#-como-baixar-o-projeto)
- [Desenvolvedores](#desenvolvido-por)

## 🔖&nbsp; Sobre
O projeto consiste em uma aplicação de teste e um relatório com definições e utilização de um ataque de força bruta. 

### Conceitos utilizados
Em um ataque de força bruta, o atacante utiliza técnicas de força bruta com o objetivo de adivinhar senhas utilizando várias combinações diferentes para se ter acesso aos dados da vítima, e a partir daí, ter acesso completo a uma conta ou sistema. Abaixo listamos alguns conceitos que foram utilizados.
1. Ataque de força bruta tradicional

    Tecnica de ataque que baseia-se na tentativa por combinação, passando por todas as combinações possíveis de caracteres até chegar em uma cadeira de caracteres específica.
2. Ataque de força bruta reversa 

    Tecnica de ataque que utiliza informações do usuário que já foram vazadas ao longo do tempo, analisando bancos de dados de e-mails e senhas. A partir daí, são testadas diferentes combinações de logins e senhas em variados serviços online.
2. Regex

    Uma forma concisa e flexível de identificar cadeias de caracteres de interesse.
3. Cluster bomb

    Tipo de ataque que usa varios payloads.

### Ferramenta de teste: Burp Suite
Descrição da ferramenta de teste

### Aplicação de teste
Foi criada uma aplicação django contendo apenas as configurações padrões e autenticação. O middleware CsrfViewMiddleware, responsável pela proteção contra Cross Site Request Forgeries, foi desativado para facilitar o ataque. 

### Como funciona?
Com a aplicação django em execução, nós criamos uma tentativa de login que foi interceptada pelo Burp Suite e então enviamos ela para a area de Intruder. Veja abaixo.
1. Na aba proxy, vá em Intercept. Com o intercept desligado, clique em Open Browser e realize uma tentativa de login no site que será atacado.
 
    ![alt text](/images/1.png)

2. Vá para a aba HTTP history e envie a requisição POST para o Intruder(ctrl+I)
![alt text](/images/2.png)

Na aba Intruder, fizemos as configurações para realizar um ataque de força bruta. Aqui consideramos duas tecnicas: A primeira, que é ataque de força bruta reversa, e a segunda, ataque de força bruta tradicional. Veja abaixo o passo-a-passo.

1. Vá para a aba Intruder e selecione a requisição que acabou de enviar.
![alt text](/images/3.png)
2. Vá em Positions, altere o tipo de ataque para Cluster Bomb e coloque entre "§" os campos que serão enviadas informações.
![alt text](/images/4.png)
3. Vá em Options, ache Grep - Extract e clique em add. Selecione algo do HTML que indique que a tentativa de login não foi bem sucedida. No nosso caso selecionamos isso:

        <p class="errornote">
            Please enter the correct username and password for a staff account. Note that both fields may be case-sensitive.
        </p>
    ![alt text](/images/5.png)

4. Vá em Payloads e selecione o tipo do payload de cada conjunto. Pode alternar entre os conjuntos em Payload Set. 
    - Caso selecione Simple list, adicione a wordlist em Payload Options;
    ![alt text](/images/6.png)
    - Caso selecione Brute Forcer, indique um conjunto de caracteres e a quantidade minima e maxima em Payload Options. Esses dados serão utilizados para formar logins e senhas.
    ![alt text](/images/7.png)

5. Agora clique em Start Attack, será aberta uma guia separa. Aguarde o ataque finalizar.
![alt text](/images/8.png)

6. Agora é possivel ordenar a lista pelas tentativas realizadas com sucesso e obter o login e senha utilizados.
![alt text](/images/9.png)
---

## 🚀 Features
- [] Descrição breve dos conceitos envolvidos
- [] Descrição da ferramenta de teste
- [x] Desenvolvimento da aplicação de teste
- [x] Descrição da utilização da ferramenta

---
## ⚒️ Tecnologias utilizadas

O projeto foi desenvolvido utilizando as seguintes tecnologias

- [Python](https://python.org)
- [Django](https://www.djangoproject.com)
- [Burp Suite](https://portswigger.net)

---

## 🗂 Como executar o projeto django
```bash
# Entre no diretorio do projeto
$ cd django_forca_bruta

# Execute as migrações do banco de dados
$ python manage.py migrate

# Crie um usuario, será necessario preencher informações
$ python manage.py createsuperuser

# Execute o servidor
$ python manage.py runserver
```

## Desenvolvido por
[Jacyiricê Silva Oliveira](https://github.com/jacyirice/)

[Rayanna Quirino](https://github.com/rayannaQuirino/)

[Rayanna Quirino](https://github.com/rayannaQuirino/)

## Disponivel em 
[GitHub](https://github.com/jacyirice/Forca-bruta)
