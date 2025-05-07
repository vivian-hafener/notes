# Jacamar CI & Gitlab runners
- Gitlab has multiple types of runner executor types --> Shell, docker, k8s, SSH, vBox, custom
- Jacamar is a HPC focused custom gitlab executor. This provides administrators a wide range of configurable options for the runner that are well-suited for HPC resources
- Jacamar-auth - manage auth for users
- Jacamar - userspace portion. Once a user is on a node, how do you run their job? Submit to a scheduler? Integrate local container runtimes? 
- Users in gitlab are associated with the job itself (user who owns the auth token / triggers ci/cd must match the user on the local HPC machine (same LDAP is preferred, though there are some ways around this. 
- Executors = supported schedulers
- Run mechanism - what runs the runner script (bash, or a container) 
- Jacamar is very powerful --> using Jacamar to run build farms and CI jobs across a very large number of resources
