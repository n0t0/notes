$ qsub <script>.sh --> add a job


$ qconf -sql --> list queues

$ qconf -sq <queue>.q --> queue's attributes

$ qstat -f --> list the cluster

```
#!/bin/bash

  #
  # -- SGE options :
  #

  #$ -S /bin/bash
  #$ -cwd
  #$ -q serial.q

  #
  # -- the commands to be executed (programs to be run) :
  #

  /bin/hostname
  /bin/date
  /bin/sleep 60
```

### Monitoring Jobs

$ qstat -u "*"

### Delete Jobs

$ qdel <1807>

### Parallel

```
#!/bin/bash

#$ -q parallel.q
#$ -pe orte.pe 16 --> every parallel job has to specify the parallel environment
```

$ qconf -spl --> list PE
$ qconf -sp <PE> --> list details

### SGE Array Job (for loop)

qsub -q docker.q -pe mpi 1 -cwd -j y -o log.txt -S /bin/bash pipeline.sh
watch qstat 
qdel <jobID>

### Flow

1. Build a Docker image with the fetch & run script
2. Push the built image to docker.ambrygen.com
3. Create a simple job script and upload it to </path/to/upload>
4. Create an <user/role> to be used by jobs to access </path/to/upload>
5. Create a job definition that uses the built image
6. Submit and run a job that execute the job script from </path/to/upload>


