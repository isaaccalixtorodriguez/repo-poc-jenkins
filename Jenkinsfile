pipeline {
    agent any

    triggers {
        githubPullRequest()
    }

    stages {
        stage('Validar con API') {
            steps {
                script {
                    def response = sh(
                        script: "curl -s -o /dev/null -w \"%{http_code}\" http://localhost:5000/validar",
                        returnStdout: true
                    ).trim()

                    if (response != "200") {
                        error("La API devolvió ${response}, fallando el build")
                    }
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Build exitoso después de la validación.'
            }
        }
    }
}
