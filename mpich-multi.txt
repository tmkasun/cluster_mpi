#include <mpi.h>
#include <stdio.h>
#include <string.h>

int main(int argc, char **argv)
{
	double num_students;
	float num_students1;
	double grade[10],grade1[10];
	char note[1024],note1[1024];
	int tag1=1001, tag2=1002;
	int rank,ncpus;
	MPI_Status status;
	
	MPI_Init(&argc,&argv);
	MPI_Comm_rank(MPI_COMM_WORLD,&rank);
	
	if(rank==0){
		num_students=23;
		strcpy(note,"Hello MPI Multi World!");
		grade[0]=100.09;
		MPI_Send(&num_students,1,MPI_DOUBLE,1,tag1,MPI_COMM_WORLD);
		MPI_Send(&grade,10,MPI_DOUBLE,2,tag1,MPI_COMM_WORLD);
		MPI_Send(&note,strlen(note)+1, MPI_CHAR,1,tag2,MPI_COMM_WORLD);		
	}

	if(rank==1){
		MPI_Recv(&num_students1,1,MPI_FLOAT,MPI_ANY_SOURCE,tag1,MPI_COMM_WORLD,&status);
		MPI_Recv(&note1,1024,MPI_CHAR,MPI_ANY_SOURCE,tag2,MPI_COMM_WORLD,&status);
		printf("Received by Rank 1 NoOfStudents %f, note %s\n",num_students1,note1);
	}

	if(rank==2){
		MPI_Recv(&grade1,10,MPI_DOUBLE,MPI_ANY_SOURCE,tag1,MPI_COMM_WORLD,&status);
		printf("Received by Rank 2 grade %f\n",grade1[0]);
		
	}

	getchar();
	return 0;

}

