# Step-1 : First set up K8s Cluster System.

# Step-2 : Now, Install Metric Server first.
-	Go to “metrics_server_files” folder inside github and apply those with K8s. <br>
  `$ kubectl apply -f .`

# Step-3 : Now Deploy Sample App. Create Service. Deploy HPA.
-	Go to “hpa_files” folder inside github and apply those manifest files with K8s. <br>
  `$ kubectl apply -f .`

# Step-4 : Notice your CPU utilisation percentage(I’d given default 50% in yml files), pod count, etc.
	$ kubectl get hpa
	$ kubectl get pods

# Step-5 : Increase Load with busybox. <br>
  `$ kubectl run -i --tty load-generator --rm --image=busybox --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://hpa-demo-deployment; done"`

# Step-6 : Monitor HPA Events.
	$ Kubectl get hpa
	$ kubectl get pods

You’ll notice, due to invoking busybox load increases…thus CPU utilisation increases, and to ensure CPU utilisation 
don’t go above 50% as mentioned in my manifest yml files, HPA will auto-scale pods. Cross check REPLICAS.<br>
Now stop busybox, and HPA will decrease count of pods automatically.
