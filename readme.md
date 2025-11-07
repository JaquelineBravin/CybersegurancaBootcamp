# Simulando um Ataque de Brute Force de Senhas com Medusa e Kali Linux

## Ambiente

- Kali Linux e Metasploitable 2, configuradas no VirtualBox, com rede interna (host-only).

## Comandos e testes

### Brute Force? Password Spraying? O que são?

Os dois são ataques a senhas de usuários, mas qual a diferença?
Enquanto o password spraying testa uma senha comum para diversos usuários, o ataque de força bruta (brute force) testa várias senhas em um único ou poucos usuários, o que pode levar ao bloqueio por números de tentativas.
O password spraying é um ataque silencioso e perigoso para quem utiliza senhas fáceis que, infelizmente, ainda são comuns.

### Simulando um serviço FTP com falhas de segurança, e tentando acessá-lo

- Descobrindo quais portas estão disponíveis através do NMAP (Imagem 1)
- Criando Wordlist com possíveis nomes de usuários e senhas comuns para tentativas de login no serviço FTP

```bash
    $ echo -e 'user\nmsfadmin\nadmin\nroot' > users.xt
    $ echo -e '123456\npassword\nqwerty\nmsfadmin' > pass.xt
```

- Rodando o ataque de força bruta utilizando Medusa diretamente ao FTP (Imagens 2 e 3)

### Rodando ataque de força bruta também em sites web utilizando Medusa

- Foi criado novamente uma Wordlist com possíveis nomes de usuários e senhas comundos, mesmo comando utilizado anteriormente
- Na imagem 4 é mostrado o comando utilizado no medusa, utilizando os parâmetros que o site utiliza para login de usuário, as tentativas de senhas com falhas e acertos, mostrando todas as possíveis combinações de acesso
- Nas imagem 9 mostra o site que foi utilizado para acesso, e logo em seguida (imagem 10) o login feito com sucesso

### Ataque em cadeia, enumeração smb e password spraying

- Foi simulado um cenário onde o serviço smb (server message block) está mal configurado. O SMB é um protocolo usado pra compartilhar arquivos, pastas, realizar autenticação de usuários entre outros.
- Comando usado para acessar o serviço (Imagem 5)
- Verificando quem são os usuários reais do sistema (enumeração de usuários, imagem 6)

Com isso é possível extrair dados reais do sistema, como nomes de contas, grupos de usuários, políticas de senha, entre outros.

- Foi criado uma Wordlist de usuários e senhas para ataque ao serviço utilizando password spraying. Realizado o ataque com o medusa, e retornado as tentativas de acesso, inclusive a de sucesso, mostrando o login e senha que foi feito a tentativa (Imagem 7)
- Testando o acesso utilizando smbclient (Imagem 8)

## O problema

Em uma situação real, estas tentativas tendo sido concluídas com sucesso, poderíam dar acesso a credenciais valiosas da empresa, também a arquivos e informações importantes e sigilosas, painel administrativo e bancos de dados.
Estes tipos de ataques não requerem grandes conhecimentos por parte do atacante, nem ferramentas difíceis de baixar e utilizar, a maioria gratuitas. Basta algo simples para que se torne perigo.

### Entendi, e agora? Como me proteger?

Agora é a hora de aumentar o nível de segurança das senhas! Há vários tipos de segurança, como por exemplo, autenticação em dois fatores, sendo essa muito eficaz pois, por mais que o invasor acerte o login e senha, ele não terá acesso ao segundo fator. Também senhas fortes e expiradas regularmente e, para implementar no sistema, há bloqueio após multiplas tentativas de login e monitoramento inteligente de logs.

Por: Jaqueline Bravin
