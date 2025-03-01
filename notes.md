# Quash Notes

# PID Q
Queue of pid_ts 
- used by jobs to keep track of current process
# Job - Any command or thing that executes
struct Queue* idq - Queue of PIDs
int job_id - job id
char* command - command string
bool background - background / not background job

# Background Job Queue
	I think we only need a list of background jobs - only ONE normal job can run at once? if im wrong, two job q's?
This should just be a queue of background jobs
# Run Script & Create Process
I think we create (schedule) all processes with create process
- and make all the complex pipes
Then we create a job from these scheduled processes with run script
- wait on PIDs of child processes to execute
## Run Script
I think should execute & create job (individual commands)
- echo "hello" - creates process with echo executable and hello argument
- echo "hello" | grep "hello" - creates two command holders:
	- one has echo and a pipe out
	- one has grep and a pipe in
	- **we connect these**
		- \# file descriptors = \# pipes
- *will want to add all pids to a job and dequeue as stuff finishes*
Wait on execution to finish
- wait using job 
## Create Process
I think should read each command holder and setup processes for correct behavior
- for pipes, open an nth file descriptor for each pipe it creates - should be able to whack this in a for loop
- redirection through dup2s / special pipes - idk how these work
fork each process to run & manage the child's fds 


