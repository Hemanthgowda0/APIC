pipeline {
    agent any
    environment {
        APIC_SERVER = 'https://us-east-1.apiconnect.cloud.ibm.com' // Trial region endpoint
        APIC_USER = 'a.l.t.a.ra.zad.i.one@gmail.com'
        APIC_PASS = 'Ssm@9916166929'
        ORG = 'api-connect-g8' // Instance name
        CATALOG = 'DEV' // Catalog name
    }
 
    stages {

        stage('Check PATH') {
            steps {
                bat 'echo %PATH%'
                bat 'apic version'
            }
        }

        stage('Checkout API Code') {

            steps {

                git branch: 'main', url: 'https://github.com/Hemanthgowda0/APIC.git'

            }

        }
 
        stage('Validate API Spec') {

            steps {

                bat 'apic validate .\\api\\ibm-sample-order-api.yaml'

            }

        }
 
        stage('Login to APIC') {

            steps {

                bat """
        apic login ^
          --server %APIC_SERVER% ^
          --username "%APIC_USER%" ^
          --password "%APIC_PASS%" ^
          --realm provider/default-idp-1
        """
            }

        }
 
        stage('Publish API to DEV Catalog') {

            steps {

                bat """
        apic publish .\\api\\ibm-sample-order-api.yaml ^
          --server %APIC_SERVER% ^
          --org %ORG% ^
          --catalog %CATALOG%
        """

            }

        }

    }

}

 
