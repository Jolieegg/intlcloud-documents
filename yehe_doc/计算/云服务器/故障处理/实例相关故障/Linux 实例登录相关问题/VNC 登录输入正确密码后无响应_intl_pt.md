## Problema
Ao tentar fazer login no CVM via VNC a mensagem a seguir é exibida mesmo que você digite a senha correta. Posteriormente, você é solicitado a inserir o nome da conta novamente.
![](https://main.qcloudimg.com/raw/13b30f4ccfc97afd0e704e2e5c600047.png)
E ao tentar fazer login remoto usando a chave SSH, a mensagem **Permission denied, please try again (Permissão negada, tente novamente)** é exibida.
![](https://main.qcloudimg.com/raw/db09e73d2a057fb8b297ffd31bf67b62.png)

## Causa comum
O arquivo de log `/var/log/btmp` está superdimensionado devido a procedimentos forçados. Este arquivo mantém logs de logins com falha. Caso ele seja muito extenso, os logs não podem ser gravados nele, o que pode causar erro de login.
![](https://main.qcloudimg.com/raw/c19f9e57a67ce6b1ed30cee22af9964c.png)

## Soluções
1. Verifique se o arquivo de log `/var/log/btmp` está superdimensionado conforme detalha o [Procedimento de solução de problemas](#ProcessingSteps).
2. Confirme se é causado por procedimentos forçados e melhore a política de segurança.

## Procedimento de solução de problemas[](id:ProcessingSteps)
1. Tente [fazer login em uma instância do CVM do Linux usando uma chave SSH](https://intl.cloud.tencent.com/document/product/213/32501).
	- Se o login for bem-sucedido, vá para a próxima etapa.
	- Se o login falhar, tente o modo de usuário único. Para mais instruções, consulte a seção [Inicialização no modo de usuário único do Linux](https://intl.cloud.tencent.com/document/product/213/34819).
2. Acesse `/var/log` e verifique o tamanho do arquivo de log `/var/log/btmp`.
3. Execute o comando a seguir para limpar o arquivo de log `/var/log/btmp` superdimensionado. Em seguida, faça o login normalmente.
```
cat /dev/null > /var/log/btmp
```
4. Verifique se o bloqueio da conta é causado por operações incorretas ou procedimentos forçados. Em último caso, recomenda-se fortalecer a política de segurança de acordo com os procedimentos abaixo:
	- Altere a senha do CVM para uma senha mais forte contendo de 12 a 16 caracteres, incluindo letras maiúsculas, letras minúsculas, caracteres especiais e números. Para mais informações, consulte a seção [Redefinição da senha da instância](https://intl.cloud.tencent.com/document/product/213/16566).
	- Exclua as contas obsoletas de login do CVM.
	- Altere a porta ssh padrão 22 para uma porta menos comum entre 1024-65525. Para mais informações, consulte a seção [Modificação da porta remota padrão de um CVM](https://intl.cloud.tencent.com/document/product/213/35376).
	- Gerencie as regras do grupo de segurança associado para abrir apenas as portas e os protocolos necessários para a sua empresa. Para mais informações, consulte [Adição de regras de grupo de segurança](https://intl.cloud.tencent.com/document/product/213/34272).
	- Feche a porta de acesso à Internet para os principais aplicativos, como os bancos de dados MySQL e Redis.
	- Instale um software de segurança (como o agente CWP), e configure alarmes em tempo real para receber avisos sobre logins suspeitos.
