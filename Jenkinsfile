pipeline {
    agent any
            stage('build') {
            // Checkout the app at the given commit sha from the webhook
            // Install dependencies, create a new .env file and generate a new key, just for testing
            sh "pwd"
            sh "cd /home/jenkins"
            sh "pwd"
            sh "wget -O /home/jenkins/nginx-0.1.12.tar.gz http://nginx.org/download/nginx-0.1.12.tar.gz" 
            //sh "cp .env.example .env"
            //sh "php artisan key:generate"

            // Run any static asset building, if needed
            // sh "npm install && gulp --production"
        }

        stage('build nginx rpm') {
            sh "mkdir -p ~/rpmbuild/{BUILD,RPMS,SOURCES,SPECS,SRPMS,tmp}"
            sh "cp ~/nginx-0.1.12.tar.gz ~/rpmbuild/SOURCES"
            sh "cp ~/nginx.spec ~/rpmbuild/SPECS"
            sh "cd ~/rpmbuild"
            sh "rpmbuild -ba ~/rpmbuild/SPECS/nginx.spec"

        }

        stage('deploy') {
            // If we had ansible installed on the server, setup to run an ansible playbook
            // sh "ansible-playbook -i ./ansible/hosts ./ansible/deploy.yml"
            sh "ansible-playbook -i /etc//ansible/hosts /etc/ansible/install.yml -u root"
			sh "rpm -qa nginx"
        }
    } 
