# Docker-Kubernetes

Apenas um aqrquivo Readme.md para que eu possa ir anotando conceitos que acho importantes. 

#Kubernetes#

Muito mais que um orquestrador de containers. Gerenciar um Cluster (conjunto de conteiners)

# Alguns conceitos rápidos: #
- Cluster: conjunto de pods
- Master: Gerenciar o cluster, manter e atualizar o estado desejado(c-manager), receber e executar os comandos (API) = Control Plane;
- node: executar os pods dentro dos nodes (Kubelets), comunicação entre os nodes (K-proxy) = Nodes; 
- KubeCtl = APi para se comunicar com a APi do central plane.
- Config Map: armazena configurações que iremos usar em determinados pods. Por exemplo, variáveis de ambiente do DB. Além disso, podemos usar um coinfig map para vários pods #desaclopamento

# O que é um pod? #

Pods são os menores e mais básicos objetos implantáveis no Kubernetes. Um pod representa uma única instância de um processo em execução no seu cluster.

Os pods contêm um ou mais contêineres, como os Docker. Quando um pod executa vários contêineres, eles são gerenciados como uma única entidade e compartilham os recursos do pod. Geralmente, executar vários contêineres em um único pod é um caso de uso avançado.

Os pods também contêm recursos compartilhados de rede e armazenamento para os contêineres:

-Rede: endereços IP exclusivos são atribuídos automaticamente aos pods. Os contêineres do pod compartilham o mesmo namespace da rede, incluindo o endereço IP e as portas de rede. Os contêineres em um pod se comunicam entre si dentro do pod em localhost.
-Armazenamento: os pods podem especificar um conjunto de volumes de armazenamento compartilhado que pode ser compartilhado entre os contêineres.

Pense em um pod como um "host lógico" autônomo e isolado que contém as necessidades sistêmicas do aplicativo que ele veicula.

Um pod destina-se a executar uma única instância do seu aplicativo em seu cluster. No entanto, não é recomendado criar pods individuais diretamente. Em vez disso, geralmente cria-se um conjunto de pods idênticos, chamado réplicas, para executar o aplicativo. Esse conjunto de pods replicados é criado e gerenciado por um controlador, como uma Implantação. Os controladores gerenciam o ciclo de vida dos pods constituintes e também podem executar escalonamento horizontal, alterando o número de pods conforme necessário.

De vez em quanto, você pode interagir com pods de maneira direta para depurar, solucionar problemas ou inspecioná-los, mas é altamente recomendável usar um controlador para gerenciá-los.

Os pods são executados em nodes no cluster. Depois de criado, o pod permanece no nó até que o processo seja concluído, o pod seja excluído, removido do nó por falta de recursos ou pela falha do nó. Se um node falhar, os pods nele serão programados para exclusão automaticamente.

Fonte: https://cloud.google.com/kubernetes-engine/docs/concepts/pod

# Criação de pods #
 Arquivo .yaml - declaração do pod. Contém as informações sobre as imagens disponiveis. Caso queira alterar, edita na IDE then kuctl apply -f PATH do yaml
    
      Para começar a edição declaramos a versão da API que pode ser a versão alfa, a versão beta e a versão estável.
      
      Onde a alfa tem coisas que podem ainda estar contendo bug; A beta que já pode ser considerada segura, mas ainda não é bom utilizar definitivamente; E a versão estável que é um “v” seguido de um número inteiro, onde é a versão estável efetivamente para uso.
      
# Services

As aplicações de microserviços  precisam se comunicar. Se um pod com o serviço de login cair, outro precisa subir no lugar dele. Porém, commo os outros serviços saberão o ip do novo pod? através do sv, que é uma abstração para expor aplicações. elas proveem Ips fixos para comunicação, DNS para um ou mais pods e são cpazes de fazer balanceamento de carga.   

OS services possuem:
-ClusterIP - serve para ele manejar o pod que ele vai enviar caso dê erro o pod atual.
-NodePort - serve para mapear a porta que ele recebe requisições de fora e que envia dentro do cluster
-Load balancer = ClusterIp + NodePOrt

São criados através de arquivos yaml






