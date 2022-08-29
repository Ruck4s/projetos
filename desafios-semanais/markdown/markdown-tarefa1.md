# Criação de buckets no GCS
Passo a passo para criação e manipulação de buckets do Cloud Storage dentro do Google Cloud Platform. <br>
A criação pode ser feita de duas maneiras:
- Via **linha de comando**
- Via **console** <br>

Porém, nesse arquivo será abordada somente via ***console***.

### 1º Passo: Instalar o SDK do Google Cloud CLI em seu terminal Debian/Ubuntu.
------
O comando que se utiliza para certificar se o SO está atendendo aos requisitos, é:
> `sudo apt-get install apt-transport-https ca-certificates gnupg`

Logo após, começa a etapa de instalação. Para isso é preciso adicionar o URI de
distribuição da CLI do Google CLoud como a origem de pacote, utilizando o comando:
> `echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] 
	https://packages.cloud.google.com/apt cloud-sdk main" | sudo 
	tee -a /etc/apt/sources.list.d/google-cloud-sdk.list`

Agora é necessário importar a chave pública do Google Cloud, com o comando a seguir:
> `curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | 
	sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -`
  
Assim, é possível instalar e atualizar a CLI gcloud, com o comando:
> `sudo apt-get update && sudo apt-get install google-cloud-cli`

*Com esse comando, além de instalar a CLI gcloud, também é instalado a linha de
comando do Cloud Storage, chamada de gsutil, que é a utilizada para realizar
ações especificamente no GCS.*

Para começar a utilizar o CLI, execute o comando:
> `gcloud init`

**O próximo passo é configurar em que projeto o terminal estará conectado.**

### 2º Passo: Configurar a CLI gcloud.
------
Agora, após executar o comando anterior, irá ser necessário fazer o login com a
conta de usuário do Google. 
> No próprio terminal é disponibilizado um link para
> permitir o acesso aos recursos do Google Cloud. <br> 
> Após permitir o acesso, será necessário selecionar um projeto no qual se tenha 
> permissão de **proprietário, editor ou leitor.** Para selecionar o projeto que deseja,
> digite o número que aparece antes do nome do projeto em si. Assim que selecionado, é possível escolher uma zona padrão do compute engine, caso
> queira. <br> 
> Após isso, a configuração do CLI está completa e você pode utilizar seu terminal para
> realizar comandos dentro do projeto selecionado no GCP. <br>

### 3º Passo: Criação do bucket no Cloud Storage.
------
Agora, para a criação e manipulação do bucket é necessário utilizar comandos do gsutil.
Para criação, se utiliza o comando:
> `gsutil mb gs://(NOME DO BUCKET)`

*Vale ressaltar que o nome do bucket é único globalmente.*

Caso queira passar parâmetros como classe do armazenamento e localidade, se utiliza
o seguinte comando:
> `gsutil mb -c (CLASSE DE ARMAZENAMENTO) -l (REGIAO DO BUCKET) on gs://(NOME DO BUCKET)`

### 4º Passo: Upload de arquivos para o bucket.
------
Para fazer upload de arquivos locais para o bucket, se utiliza o comando:
> `gsutil cp (CAMINHO DO ARQUIVO) gs://(NOME DO BUCKET)/`

Já para copiar arquivos de um bucket para outro, se utiliza o comando:
> `gsutil cp gs://(NOME DO BUCKET C/ ARQUIVO)/(NOME DO ARQUIVO) gs://(NOME DO BUCKET DE DESTINO)/(NOME DA CÓPIA)`

Para fazer o download de um arquivo no bucket para a maquina local, se utiliza o comando:
> `gsutil cp gs://(NOME DO BUCKET)/(NOME DO ARQUIVO) (CAMINHO LOCAL)`

Para listar os buckets se utiliza o comando:
> `gsutil ls`

E para listar os objetos do bucket se usa:
> `gsutil ls gs://(NOME DO BUCKET)/`

### 5º Passo: Deletar buckets.
------
Para deletar os buckets de forma recursiva se utiliza o comando:
> `gsutil rm -r gs://(NOME DO BUCKET)`

Desse modo é apagado o bucket e os objetos que tinham dentro dele.

*Vale ressaltar que assim que apagado, o nome utilizado passa a se tornar disponível
novamente.*

### Considerações finais.
------
As informações apresentadas daqui foram extraídas da documentação da própria ferramenta, e caso necessite de mais detalhes
consulte: https://cloud.google.com/storage/docs/discover-object-storage-console?hl=pt-br

*Futuramente um guia para a criação de um bucket no console do GCP será desenvolvido para assim ter ambas as opções de criação.*

![Google Cloud Platform](https://raw.githubusercontent.com/Ruck4s/projetos/main/desafios-semanais/markdown/Logo%20GCP.png)
