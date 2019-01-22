pipeline {
    agent {
        label 'backup'
    }
   stages {
    stage ('Template Creation') {
        steps {
            withCredentials([file(credentialsId: 'backup', variable: 'BACKUP')]) {
                sh """
                    rm -f backup.py
                    cp $BACKUP backup.py
                    chmod a+x backup.py
                    ./backup
                """
            }
          }
        }
    stage ('Send mail') {
        steps {
            emailext body: 'Backup created as requested', subject: 'Automated Backup', to: 'noha.fahmy1@vodafone.com'
          }
        }
    }
}
