# ansible-confluent-kafka-install

This playbook will help you install kafka brokers and zookeeper cluster on separate nodes 3+3 by default unless specify the variables.
Also creates keystore for ssl_mode='yes' if specified and required your root.crt and root.key to be placed in install/roles/files/

This playbook Installs Confluent Community Kafka platform version oss-2.11

From best practices document from confluent-kafka documentation

![alt text](https://github.com/geeksinsights/ansible-confluent-kafka-install/blob/master/Kakfa-multinode-cluster.JPG)

**Install Playbook**
   
      git clone repository

**HostFile structure, so that roles will be called accordingly.**
   
   - **For Kafka broker**

         [kafka]
         prodkafka01.localdomain
         
         prodkafka02.localdomain
         
         prodkafka03.localdomain

   
   - **For Zookeeper nodes**
   
         [zookeeper]
 
         prodzookeep01.localdomain
         
         prodzookeep02.localdomain
         
         prodzookeep03.localdomain


**Run playbook**

   - **Modify variables below and run, this will install kafka brokers and zookeepers on speficied hosts in hosts file**


         ansible-playbook -i hosts install/kafka.yml



**Variables File install/group_vars/kafka_vars.yml**

   **User to run the playbook**

      ansible_system_user: root

   **EPEL Repository for extra packages**

     epel_repo: https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

     java_home: /usr/lib/jvm/jre-1.8.0-openjdk

   **SSL Params if no below will be ignored**

     ssl_mode: Yes

     keystore_password: inputpasswordhere

     key_password: inputpasswordhere

     truststore_password: inputpasswordhere

     keystore_path: /etc/kafka/

     key_file: server.key

     cert_file: server.crt

     chain_file: server.crt

     truststore_name: kafka_truststore.jks

     keystore_name: kafka_keystore.jks

   **Zookeeperlist - Provide list in form of node1:2181,node2:2181**

     zookeeper_node_list: prodzookeep01.localdomain:2181,prodzookeep02.localdomain:2181,prodzookeep03.localdomain:2181

     zoonode1: prodzookeep01

     zoonode2: prodzookeep02

     zoonode3: prodzookeep03
     
     multinode: Yes

   **DataDirectories**

     zookeeper_directory: /zookeeper/data/

     kafka_directory: /kafka1/data/,/kafka2/data/,/kafka3/data/,/kafka4/data/,/kafka5/data/

   **domain variable if nothing keep localdomain**

     domain: localdomain

   **environment**

     env: prod

   **set memory of your requirement in gb**

     memory_gb: 32
