# inspec-cfgmgmtcamp-ghent-2019
The InSpec examples for Config Management Camp 2019 - presented by Gratien D'haese

## Pre-requisites
- Linux or Mac OS/X system
- vim editor or alike
- docker
- vagrant
- Oracle VirtualBox
- InSpec from Chef
- git (to clone this git repo: https://github.com/gdha/inspec-cfgmgmtcamp-ghent-2019)

## Start of docker mychefdf
- go to directory inspec-cfgmgmtcamp-ghent-2019/docker-chefdk
- run: ./build-chefdk
- run: ./run-chefdk
- (inside the container) run: inspec exec /cookbooks/myaccount/test/integration/default/default_test.rb

## In another Bash shell windows (on your Linux or Mac)
- go to directory inspec-cfgmgmtcamp-ghent-2019/cookbooks/myaccount/test/integration/default 
- run: docker ps -a
- run: docker rename $(docker ps -q) inspec-demo
- run: docker ps -a
- run: inspec exec default_test.rb -t docker://$(docker ps -q)

## Remediate the mychefdk container with chef cookbook myaccount
- (inside the container) run: chef-client -z -o myaccount
- (inside the container) run: inspec exec /cookbook/myaccount/test/integration/default/default_test.rb
- (on Mac) run: inspec exec default_test.rb -t docker://$(docker ps -q)

## Demonstrate the dockerprofile
- go to directory inspec-cfgmgmtcamp-ghent-2019/
- (on Mac) run: inspec exec dockerprofile/controls/docker.rb
- run: docker rename $(docker ps -q) inspec-demo
- (on Mac) run: inspec exec dockerprofile/controls/docker.rb
- (on Mac) run: inspec exec dockerprofile

## Demonstrate InSpec Shell
- (on Mac) if container runs in detached mode run: docker exec -it inspec-demo /bin/bash
- (inside the container) run: inspec shell
- (inside the container) run: inspec> help
- (inside the container) run: inspec> command('uname -s').stdout
- (inside the container) run: inspec> describe file('/etc/gshadow') do
- (inside the container) run: inspec>   it { should be_owned_by 'root' }  
- (inside the container) run: inspec> end 

## Demonstrate InSpec profile
- (inside the container) run: inspec init profile newprofile
- (inside the container) run: inspec check newprofile

