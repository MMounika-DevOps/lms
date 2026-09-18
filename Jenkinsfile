stage('Start Database') {
    steps {
        echo 'Starting MySQL database...'

        sh '''
            docker compose up -d db
        '''

        echo 'Waiting for MySQL to become ready...'

        sh '''
            for i in $(seq 1 30); do
                if docker compose exec -T db mysqladmin ping -h 127.0.0.1 -uroot -ppassword --silent; then
                    echo "MySQL is ready!"
                    exit 0
                fi

                echo "MySQL is not ready yet... waiting..."
                sleep 2
            done

            echo "MySQL did not become ready."
            docker compose logs db
            exit 1
        '''
    }
}
