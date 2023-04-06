# apache-prometheus-grafana

You can setup a prometheus-grafana monitoring setup which will collect apache and prometheus metrics and show it on grafana in visual graphs.

first you have to setup an apache server in minikube 

kubectl create -f apache.yml  

After that You have to setup apache-exporter which will collect metrices from apache and export it to prometheus.

kubectl create -f apache-exporter.yml
kubectl create -f apache-metrices-svc.yml

Now you have to setup prometheus.By default prometheus uses prometheus.yml file for configuration and we can create configmap to override
or implement changes in configuration.So we will create a configmap.

kubectl create -f prometheus-configmap.yml          ## we will mount this configmap in prometheus-deployment.yml file                                       Kubectl create -f prometheus-deployment.yml         ##  so that we can add targets in prometheus.yml

Now setup grafana 

kubectl create -f grafana.yml

This will create whole monitoring Setup.

Now login to grafana and add prometheus as Datasource.You have to enter the url of prometheus in datasource.After successfully adding prometheus as 
data source you can import dashboards from grafana's official website or create one by yourself.