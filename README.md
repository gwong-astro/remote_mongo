# Remote access of Jupyter notebook and Mongo services on ICRAR servers

The steps to remotely run mongo and jupyter notebook on ICRAR servers and scripts used to access Mongo services via python package pymongo 


### Setting up services on remote server
Substitute 'user' with your user name. 

ssh -Y user@hyrmine.icrar.org

To install mongo you can use the container version (singularity) of Mongo (see https://github.com/singularityhub/mongo).
The container is created in the directory mongo.  Use screen/tmux to start up the various services.


cd mongo

#### Start up the primary daemon process for the MongoDB system (mongod)

screen -S mongod
singularity exec --bind /scratch/mongo_data:/data/db mongo.sif mongod

##### Detach from the exisiting screen session
Ctrl+a d

#### Start the interactive JavaScript interface to MongoDB (mongo)

screen -S mongo
singularity exec --bind /scratch/mongo_data:/data/db mongo.sif mongo

##### Detach from the exisiting screen session again
Ctrl+a d

#### startup jupyter notebook
screen -S notebook
jupyter notebook --no-browser --port=9001

##### Detach from the exisiting screen session again
Ctrl+a d


### Remote connection (port forward)
#### On a new localhost terminal
ssh -N -L 8899:localhost:9001 user@hyrmine.icrar.org



### Screen quick reference 
Resume session: screen -r NAME
List out exisiting Sessions: screen -ls


