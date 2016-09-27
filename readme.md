High Performance Computing Cluster
==================================

Based on: https://help.ubuntu.com/community/MpichCluster

Examples
=======
Change directory to your mirror folder and write this MPI helloworld program in a file mpi_hello.c 

Compile it:

mpiu@ub0:~$ mpicc mpi_hello.c -o mpi_hello

and run it (the parameter next to -n specifies the number of processes to spawn and distribute among nodes):

mpiu@ub0:~$ mpiexec -n 8 -f /home/mpiu/machinefile ./mpi_hello

You should now see output similar to this:

Hello from processor 0 of 8
Hello from processor 1 of 8
Hello from processor 2 of 8
Hello from processor 3 of 8
Hello from processor 4 of 8
Hello from processor 5 of 8
Hello from processor 6 of 8
Hello from processor 7 of 8