# Agentify

Create jenkins jnlp agent from *any image. 

setup for kubernetes jnlp pod: 

```
Pod Template
 	Name	
<node name>
 	Namespace	
<k8n namespace>
 	Labels	
<node label>
 	Usage	
Only build jobs with label expressions matching this node
 	Pod template to inherit from	
 	Containers	
Container Template
 	Name	
jnlp
 	Docker image	
<this image location>
 	Always pull image	
 	Working directory	
/home/jenkins/agent
 	Command to run	
 	Arguments to pass to the command	
${computer.jnlpmac} ${computer.name} 
 	Allocate pseudo-TTY	
checked

```

if you want to also use nested nodes ( for example for parallel runs)

you need to set another container with same name as pod template name

```

Container Template
 	Name	
<node name
 	Docker image	
<image locaiton>
 	Always pull image	
 	Working directory	
/home/jenkins/agent
 	Command to run	
/bin/bash -c
 	Arguments to pass to the command	
cat
 	Allocate pseudo-TTY	
checked
```

and do this little trick: 

```
    this.steps.functions.node = this.steps.functions.container
```
