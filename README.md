# Hbase

- [1. Descrição](#link1)
- [2. Instalação](#link2)
- [3. Comandos básicos](#link3)
- [4. Links](#link4)

<a id="link1"></a>
## 1. Descrição

O Apache HBase é um banco de dados NoSQL colunar que permite operações de leitura e gravação em grandes datasets.

HBase é uma implementação do Google’s Bigtable.

Diferenciais:

- Maior compressão</br>
os dados de tipos iguais são armazenados juntos, há uma otimização de espaço utilizado</br>
- Eliminação da necessidade de índices</br>
não é necessário rearranjar como as cores de blocos estão ordenadas (existem outras opções de otimização como sharding)</br>
- Alta-performance para operações de agregação

<a id="link2"></a>
## 1. Instalação

A instalação do Hbase pode ser realizada de 3 formas:</br>
- Hbase - Standalone mode installation (sem usar o hdfs)
- Hbase - Pseudo Distributed mode of installation (usando o hdfs em um node apenas)
- Hbase - Fully Distributed mode installation (usando o hdfs em um cluster)

Versões usadas:
- hadoop 2.6.4
- hbase 1.2.0

#download</br>
wget https://archive.apache.org/dist/hbase/1.2.0/hbase-1.2.0-bin.tar.gz

![Screenshot](/images/h01.jpg)

#extract</br>
```tar xvzf hbase-1.2.0-bin.tar.gz```

#mover para a pasta destino e permissões para o usuário padrão</br>
```sudo mv hbase-1.2.0 /usr/local/hbase```</br>
```sudo chown -R hduser /usr/local/hbase```</br>

![Screenshot](/images/h02.jpg)

## Configuração

#criar pasta zookeeper para armazenar dados</br>
```mkdir /usr/local/hbase/zookeeper```</br>

#editar bashrc</br>
```sudo nano ~/.bashrc```</br>
```export HBASE_HOME=/usr/local/hbase```</br>
```export PATH=$PATH:/usr/local/hbase/bin```</br>
```source ~/.bashrc```</br>

![Screenshot](/images/h03.jpg)

#editar arquivo hbase-env.sh e acrescentar</br>
```nano /usr/local/hbase/conf/hbase-env.sh```</br>

```export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-arm64```</br>
```export HBASE_REGIONSERVERS=/usr/local/hbase/conf/regionservers```</br>
```export HBASE_MANAGES_ZK=true```</br>

![Screenshot](/images/h04.jpg)

#editar hbase-site.xml e acrescentar
```nano /usr/local/hbase/conf/hbase-site.xml```

![Screenshot](/images/h05.jpg)

#start hadoop daemons</br>
```start-dfs.sh```</br>
```start-yarn.sh```</br>

![Screenshot](/images/h06.jpg)

#start hbase daemon</br>
```start-hbase.sh```</br>

![Screenshot](/images/h07.jpg)

#usar jps para conferir o serviço</br>

![Screenshot](/images/h08.jpg)

#pasta hdfs criada com sucesso</br>
```hdfs dfs -ls /hbase```</br>

![Screenshot](/images/h09.jpg)

Acessando a Web Interface do HBase

http://slave3:16010/</br>

![Screenshot](/images/h10.jpg)

<a id="link3"></a>
## 3. Comandos básicos

Para interagir com o Hbase podemos usar o shell ou API Java.</br>

- shell</br>
```hbase shell```</br>

![Screenshot](/images/h11.jpg)

```status```</br>
```version```</br>
```whoami```</br>

![Screenshot](/images/h12.jpg)

- create table</br>
```create 'employee', 'personal data', 'professional data'```

![Screenshot](/images/h13.jpg)

- inserir dados</br>
```put 'employee','1','personal data:first_name','Reena'```</br>
```put 'employee','1','personal data:last_name','Basten'```</br>
```put 'employee','1','personal data:city','Lelystad'```</br>
```put 'employee','1','professional data:designation','Professor'```</br>
```put 'employee','1','professional data:salary','5000'```</br>

![Screenshot](/images/h14.jpg)

- scan</br>
```scan 'employee'```

![Screenshot](/images/h15.jpg)

- list</br>

![Screenshot](/images/h16.jpg)

- describe</br>
```describe 'employee'```

![Screenshot](/images/h16.jpg)

<a id="link4"></a>
## 4. Links

Apache Hbase</br>
http://hbase.apache.org/</br>

Apache Hbase downloads</br>
https://downloads.apache.org/hbase/</br>

Banco colunar</br>
https://aws.amazon.com/pt/nosql/columnar/</br>