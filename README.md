# Workfolw
Step 1  Added Basic yml file without checkout synatx
Added first-example yml to display some message and list files in repo and dispaly content in readme file
it failed because didn't added checkout step

Step 2  added checkout syntax
Added checkout file and pushed again. It worked now
Ckeckout action step will tell workflow to clone repository files to runner  environment

Step 3 created new workfloe to generate ascii artwork
Added commands to generate ASCII Artwork usomg cowsay. It failed becoause cowsay is thord party library and we didnt added third party library in workflow.

Step 4 added third party libraries to install ascii artwork
Added third party library using htis cmnds - name: Install Cowsay Program run: sudo apt-get install cowsay -y , and pushed code it worked properly and displayed dragon ascii artwork

Step 5  craeated seperate shell script file to generate ascii and called in workflow file
executed same ascii artwork using shell script by below process
gave all commands to install cowsay and display dragon in a script file and called that file in workflow yml file using this commands      - name: executing shell script run: ./ascii-script.sh(should call file in this format if file is in repository not in workflows folder) Note: i have created ascii.script.sh in .github/workflows  folder not in Workfolw repository so above synatx gave error
Syntax to give if created files under same yml folder is - name: executing shell script run: |(pipe symbol to pass multiple commands ata time)  chmod +x .github/workflows/ascii-script.sh enter .github/workflows/ascii-script.sh
chmod is used to pass permissions because default permissions are only read permissions and we cannot execute shell script file with read permissions. so with chmod we are pproviding executing permission.

Step 6 modified generate cowsay to add multiple jobs in workflow
Added 3 jobs build_job_1, test_job_2, deploy_job_3  to bulid, test and deploy ascii artwork as we do in CI/CD process, and pushed code it will fail because test and deploy jobs are dependent on bulid jobs o/p file.
By default in multiple jobs, jobs are not dependent on each other, each job will run on its own, so in this case test and deploy jobs completed first and build job later as jobs by default do not wait for other jobs to complete so only run failed.

Step 7 Added Needs command to make jobs dependent on each other
