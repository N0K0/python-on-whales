# The Docker client object


{{autogenerated}}

# Sub-commands
* [`docker.app`](sub-commands/app.md)
* [`docker.buildx`](sub-commands/buildx.md)
* [`docker.compose`](sub-commands/compose.md)
* [`docker.config`](sub-commands/config.md)
* [`docker.container`](sub-commands/container.md)
* [`docker.context`](sub-commands/context.md)
* [`docker.image`](sub-commands/image.md)
* [`docker.manifest`](sub-commands/manifest.md)
* [`docker.network`](sub-commands/network.md)
* [`docker.node`](sub-commands/node.md)
* [`docker.secret`](sub-commands/secret.md)
* [`docker.service`](sub-commands/service.md)
* [`docker.stack`](sub-commands/stack.md)
* [`docker.swarm`](sub-commands/swarm.md)
* [`docker.system`](sub-commands/system.md)
* [`docker.trust`](sub-commands/trust.md)
* [`docker.volume`](sub-commands/volume.md)


# Other commands

They're actually aliases

* [`docker.build`](sub-commands/buildx.md#build)
* [`docker.commit`](sub-commands/container.md#commit)
* [`docker.copy`](sub-commands/container.md#copy)
* [`docker.create`](sub-commands/container.md#create)
* [`docker.diff`](sub-commands/container.md#diff)
* [`docker.execute`](sub-commands/container.md#execute)
* [`docker.export`](sub-commands/container.md#export)
* [`docker.images`](sub-commands/image.md#list)
* [`docker.import_`](sub-commands/image.md#import_)
* [`docker.info`](sub-commands/system.md#info)
* [`docker.kill`](sub-commands/container.md#kill)
* [`docker.load`](sub-commands/image.md#load)
* [`docker.logs`](sub-commands/container.md#logs)
* [`docker.pause`](sub-commands/container.md#pause)
* [`docker.ps`](sub-commands/container.md#list)
* [`docker.pull`](sub-commands/image.md#pull)
* [`docker.push`](sub-commands/image.md#push)
* [`docker.rename`](sub-commands/container.md#rename)
* [`docker.restart`](sub-commands/container.md#restart)
* [`docker.remove`](sub-commands/container.md#remove)
* [`docker.run`](sub-commands/container.md#run)
* [`docker.save`](sub-commands/image.md#save)
* [`docker.start`](sub-commands/container.md#start)
* [`docker.stats`](sub-commands/container.md#stats)
* [`docker.stop`](sub-commands/container.md#stop)
* [`docker.tag`](sub-commands/image.md#tag)
* [`docker.top`](sub-commands/container.md#stop)
* [`docker.unpause`](sub-commands/container.md#unpause)
* [`docker.update`](sub-commands/container.md#update)
* [`docker.wait`](sub-commands/container.md#wait)


# About multithreading and multiprocessing

Behind the scenes, Python on whales calls the Docker command line interface with
subprocess. The Python on whales client does not store any intermediate state so it's safe 
to use with multithreading. 

The Docker objects store some intermediate states (the attributes 
that you would normally get with `docker ... inspect`but no logic in 
the codebase depends on those attributes. They're just here so that users can look at them. 
So you can share them between process/threads and pickle containers, images, networks...

The Docker daemon works with its own objects internally and handles concurrent and conflicting requests. 
For example, if you create two containers with the same name from different threads, only one will 
succeed. If you pull the same docker image from multiple processes/threads, the Docker daemon will 
only pull the image and layers once.

Just be careful with some scenario similar to this one

```
Thread 1: my_container = docker.run(..., detach=True)
...
# my_container finishes
...
Thread 2: docker.container.prune()
...
Thread 1: docker.logs(my_container)  # will fail because the container was removed by thread 2
```

In the end, unless you use this type of logic in your code, 
Python-on-whales is safe to use with multithreading and multiprocessing.
