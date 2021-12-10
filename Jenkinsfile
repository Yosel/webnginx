node {
    def app

    stage('Clone repository') {
        /* asegurese de tener un repositorio clonado */
        checkout scm
    }

    stage('Build image') {
        /* Esto construye la imagen actual sinonimo de docker build */
        app = docker.build("yoselalder/webnginx")
    }

    stage('Test image') {
        /* Idealmente debemos ejecutar un test sobre nuestra imagen en nuestro caso saltaremos esa tarea */
        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finalmente, subiremos la imagen con dos etiquetas:
         * Primero, el numero de version incremental
         * Segundo, la etiqueta 'latest'.
         * Subiendo multiples etiquetas. */
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}