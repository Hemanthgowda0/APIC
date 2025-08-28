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

        stage('Checkout API Code') {

            steps {

                git branch: 'main', url: 'https://github.com/your-org/your-api-repo.git'

            }

        }
 
        stage('Validate API Spec') {

            steps {

                sh 'apic validate ./api/ibm-sample-order-api.yaml'

            }

        }
 
        stage('Login to APIC') {

            steps {

                sh '''

                apic login \

                  --server $APIC_SERVER \

                  --username "$APIC_USER" \

                  --password "$APIC_PASS" \

                  --realm provider/default-idp-1

                '''

            }

        }
 
        stage('Publish API to DEV Catalog') {

            steps {

                sh '''

                apic publish ./api/ibm-sample-order-api.yaml \

                  --server $APIC_SERVER \

                  --org $ORG \

                  --catalog $CATALOG

                '''

            }

        }

    }

}

 
