pipeline {
  agent {
    docker {
      image 'library/mariadb:10.3'
      // run as root user
      args '-u root'
      reuseNode true
    }
  }
  environment {
    DATABASES_HOST = '192.168.50.226'
    DATABASES_PORT = '3306'
    DB_CREDENTIALS = credentials('mariadb-credentials')
  }
    stages {
        stage('Connect to mariadb client container and show databases') {
            steps {
                sh """
                    mysql \
                    --host=\$DATABASES_HOST \
                    --port=\$DATABASES_PORT \
                    
                    -password=\$DB_CREDENTIALS_PSW \
                    -e 'SHOW DATABASES;'
                """
            }
        }

        // stage('Create migrations database') {
        //     steps {
        //         sh """
        //             mysql -h \$DATABASES_HOST -P \$DATABASES_PORT -u\$DB_CREDENTIALS_USR -p\$DB_CREDENTIALS_PSW -e "
        //                 CREATE DATABASE IF NOT EXISTS db_migrations;
        //                 GRANT ALL PRIVILEGES ON `db_migrations`.* TO '\$DB_CREDENTIALS_USR'@'%';
        //             "
        //         """
        //     }
        // }

        // stage('Use migrations database and create migrations table') {
        //     steps {
        //         sh """
        //             mysql -h \$DATABASES_HOST -P \$DATABASES_PORT -u\$DB_CREDENTIALS_USR -p\$DB_CREDENTIALS_PSW -e "
        //                 USE db_migrations;
        //                 CREATE TABLE IF NOT EXISTS schema_migrations (
        //                     id INT AUTO_INCREMENT PRIMARY KEY,
        //                     filename VARCHAR(255) NOT NULL UNIQUE,
        //                     applied_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
        //                 );
        //                 SHOW tables;
        //             "
        //         """
        //     }
        // }


    // stage('Apply migrations') {
    //   steps {
    //     sh """
    //       for file in \$(ls ./migrations/*.sql | sort); do
    //         FILENAME=$(basename "$file")
    //         echo "Checking migration: ${FILENAME}"
    //         APPLIED=$(docker exec -i ${MARIADB_CLIENT_CONTAINER_NAME} mysql -h ${DATABASES_HOST} -P ${DATABASES_PORT} -u${DB_CREDENTIALS_USR} -p${DB_CREDENTIALS_PSW} db_migrations -e "
    //           SELECT COUNT(*) FROM schema_migrations WHERE filename='${FILENAME}';
    //         " | tail -n 1)
    //         if [ ${APPLIED} -eq "0" ]; then
    //             echo "Applying migration: ${FILENAME}"
    //             docker exec -i ${MARIADB_CLIENT_CONTAINER_NAME} mysql -h ${DATABASES_HOST} -P ${DATABASES_PORT} -u${DB_CREDENTIALS_USR} -p${DB_CREDENTIALS_PSW} my-maria-database < \$file
    //             docker exec -i ${MARIADB_CLIENT_CONTAINER_NAME} mysql -h ${DATABASES_HOST} -P ${DATABASES_PORT} -u${DB_CREDENTIALS_USR} -p${DB_CREDENTIALS_PSW} db_migrations -e "
    //               INSERT INTO schema_migrations (filename) VALUES ('\$FILENAME');
    //             "
    //         else
    //             echo "Migration already applied: ${FILENAME}"
    //         fi
    //       done
    //     """
    //   }
    // }
    }

    
  // post {
  //   always {
  //     sh '''
  //       docker stop ${MARIADB_CLIENT_CONTAINER_NAME}
  //     '''
  //   }
  // }
}
