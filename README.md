# Docker-Kubernetes

Apenas um aqrquivo Readme.md para que eu possa ir anotando conceitos que acho importantes. 

#Kubernetes

Muito mais que um orquestrador de containers. Gerenciar um Cluster (conjunto de conteiners)

- Pods: conteiner encapsulado 
- Master: Gerenciar o cluster, manter e atualizar o estado desejado(c-manager), receber e executar os comandos (API) = Control Plane;
- node: executar os pods dentro dos nodes (Kubelets), comunicação entre os nodes (K-proxy) = Nodes; 

- KubeCtl = APi para se comunicar com a APi do central plane.
