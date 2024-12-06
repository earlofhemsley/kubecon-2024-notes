# Open Source RDS

When life gives you containers, make an open source RDS ... a K8s love story
"If you think of yourself as a person who makes decisions based on data, you're still going to make a lot of emotional decisions"

## Topic: DBs as a service

This is a narrative. This outlines his journey as he tried to run a db in k8s.

DBis in k8s? Big no no. k8s is for stateless!

3 reasons why someone would run data in k8s
 - Stragegy
     - Cloud neutrality ... you can run your same db anywhere you like
     - No vendor-lock
 - Cost
     - If you do it right, it's no only about your infra, but it's also about cost in terms of spent eng hrs / opportunity costs
 - Automation
     - you can automate all sorts of things in k8s. Why not dbs as well?
     - blue/green
     - failovers, etc.

Fears about running dbs in k8s
 - Performance. "It'll be slow!!"
     - it's really not any slower. The performance is as good as the hardware within 1%
 - Maturity
     - Is it mature enough to run dbs?
 - Complexity
     - K8s is a complex beast with a learning curve
     - Adding Dbs on top of that seems less than ideal.

### Chapter 1: Enthusiasm and k8s 101

you run your db in k8s
dbs are stateful, so you need storace
pvc persistent volume claim ... this is how you provide storage
now i want to connect to the database. so i add a service. No LB, no ports, nothing special. Just a control plane to connect.
Now i need username/passwords ... so I add secrets and config maps, which are two well-known k8s contructs
Hey, stateful sets are a thing, so let's put the db into the stateful set!
Now I need availabily. How do I do that? Add another pod into the stateful set! Now I have db replication!
What about failover? What if something fails and I need to roll things! "HA magic" handle that. But now in order to do that, I need a proxy/balancer.

Woof. Very complex.

IaC to the rescue! I can use helm and argo and terraform to abstract all this stuff and with a simple command, i have everything.

### Chapter 2: Disillusionment and operators 101

Deployment is the smallest task. Management is difficult. Upgrades. Scaling. Failing over. Backups. Monitoring. Maintainance. etc.
Operators are intended to make management much more simple. They are a thing that can help us with that. 
Presenter represents Percona. Percona is an operator company. They provide operators.
You write an operator manifest, send it to the operator in the cluster, and the operator will do everything to deploy and manage the db.
Operators are building blocks. There are many. Like Strimzi, Percona, Redis, CloudNativePG.
Even so, you need to understand how the operator works. These things are self-service.
 - There's no UI/API. You have to configure this stuff. 
 - Not multi-cluster. you're stuck within a single k8s cluster
 - Manual integrations.


### Chapter 3: Open Source DBaaS
Percona DBaaS. Percona brought all this stuff together to provide DBaaS

Components to their architecture
 - WEB UI: React/MUi
 - API: GoLang
 - Everest operator: Unified custom resource definition via yaml manifests.
     - One operator to rule them all
     - There's only one operator to work with as opposed to having to learn operators for each particular db flavor
 - Operator lifecycle manager

### Observations / Problems to be overcome

Everest cannot be UI for operators. 
 - It's more like an API for operators with a pretty UI face.
 - Too many custom resources to factor in in terms of the many sub operators to manage
 - Other integrations?

Reinvent authentication? 
- They tried to use Zitadel, it didn't work. It became _way_ too complex.
- The ended up going with self-rolled OIDC inside of k8s.

Pluggability leads to more value
 - Everest really only supports Percona operators right now. 
 - If they wanted to support other operators to add other dbs, there's a long runway and heavy lift to that.

