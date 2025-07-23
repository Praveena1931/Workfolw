# Workfolw
Step 1  Added Basic yml file without checkout synatx --action no 5 (First-example.yml)
Added first-example yml to display some message and list files in repo and dispaly content in readme file
it failed because didn't added checkout step

Step 2  added checkout syntax --action no 7 (First-example.yml)
Added checkout file and pushed again. It worked now
Ckeckout action step will tell workflow to clone repository files to runner  environment

Step 3 created new workflow to generate ascii artwork --action no 1 (generate-cowsay.yml)
Added commands to generate ASCII Artwork usomg cowsay. It failed becoause cowsay is thord party library and we didnt added third party library in workflow.

Step 4 added third party libraries to install ascii artwork --action no 2 (generate-cowsay.yml)
Added third party library using htis cmnds - name: Install Cowsay Program run: sudo apt-get install cowsay -y , and pushed code it worked properly and displayed dragon ascii artwork

Step 5  craeated seperate shell script file to generate ascii and called in workflow file --action no 10 (generate-cowsay.yml)
executed same ascii artwork using shell script by below process
gave all commands to install cowsay and display dragon in a script file and called that file in workflow yml file using this commands      - name: executing shell script run: ./ascii-script.sh(should call file in this format if file is in repository not in workflows folder) Note: i have created ascii.script.sh in .github/workflows  folder not in Workfolw repository so above synatx gave error
Syntax to give if created files under same yml folder is - name: executing shell script run: |(pipe symbol to pass multiple commands ata time)  chmod +x .github/workflows/ascii-script.sh enter .github/workflows/ascii-script.sh
chmod is used to pass permissions because default permissions are only read permissions and we cannot execute shell script file with read permissions. so with chmod we are pproviding executing permission.

Step 6 modified generate cowsay to add multiple jobs in workflow --action no 11 (generate-cowsay.yml)
Added 3 jobs build_job_1, test_job_2, deploy_job_3  to bulid, test and deploy ascii artwork as we do in CI/CD process, and pushed code it will fail because test and deploy jobs are dependent on bulid jobs o/p file.
By default in multiple jobs, jobs are not dependent on each other, each job will run on its own, so in this case test and deploy jobs completed first and build job later as jobs by default do not wait for other jobs to complete so only run failed.

Step 7 Added Needs command to make jobs dependent on each other --action no 12 (generate-cowsay.yml)
added needs: syntax for test and deploy jobs so that multiple jobs run in sequence.after pushing test job awill fail because its dependent on build jobs o/p file. By default o/p files are not accessible within jobs we have to provide artifacts commands to access files from one job to another job
As the test job failed deploy job will be skipped because it is dependent on test job

Step 8 Sharing files from one job to another
to store data once a workflow is completed you can use *upload artifact* and use that stored o/p in another job use *download  atrifact*  added upload artifact in build to store o/p file and download artifact in test and deploy to use that stored o/p file