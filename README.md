## kubecron
A simple kubernetes cron system


## Description

A simple kubernetes cron system based on the google/cloud-sdk image. The main idea is to have a running pod, that will execute commands, and also have inside it the kubectl tools. 

You can build periodic tasks that manage your app or your cluster.

- Every task is a shell script / program binary ... like (bin/show_pods.sh)
- You program them, thtrough adding it to cron.json
- The format for the time, is based on github.com/robfig/cron
- Every time you need to update the cron, just build a new container, 
and update your rc.


## Howto

- Create your script and add them to bin
- Add the entry to cron.json, format:

```
{
  "cmd": "/bin/show_pods.sh",
  "when": "@every 2h"
}
```

- Install your cron on kubernetes (Must be done only the first time)
  Add your docker image to k8.yml and make create_rc

  check that the pod is present:
```
  kubectl get rc kubecron
```

- Update: 
  Add your scripts, and run make update
  This will recreate your image, push it and do a rolling-update

- Develop:
  For recompiling, or changing the cron.go, you will need a go dev env, 
  and source the init.sh first . (This will add src/tmpo.io to your GOPATH)
  
   
     
