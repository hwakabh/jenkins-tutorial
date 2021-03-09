pipeline {
    agent {
        label 'master'
    }
    environment {
        JMETER_DOWNLOAD_URL='https://ftp.jaist.ac.jp/pub/apache//jmeter/binaries/apache-jmeter-5.4.1.tgz'
        JMETER_DOWNLOAD_PATH='/var/jenkins_home/ci-workspace/jenkins'
        JMETER_DOWNLOAD_FILENAME='apache-jmeter.tgz'
        JMETER_BINARY_PATH='/var/jenkins_home/ci-workspace/jmeter'
        JMETER_JMX_PATH='/var/jenkins_home/ci-workspace/jmeter/example.jmx'
        JMETER_RESULT_PATH='/var/jenkins_home/ci-workspace/jmeter/example_result.jtl'
    }
    stages {
        stage('Download Jmeter Binaries') {
            steps {
                sh """
                    mkdir -p $JMETER_DOWNLOAD_PATH
                    curl --output $JMETER_DOWNLOAD_PATH/$JMETER_DOWNLOAD_FILENAME $JMETER_DOWNLOAD_URL
                    ls -al $JMETER_DOWNLOAD_PATH/$JMETER_DOWNLOAD_FILENAME
                """
        }
        }
        stage ('Setup JMeter CLI') {
            steps {
                sh """
                    mkdir -p $JMETER_BINARY_PATH
                    tar xzvf $JMETER_DOWNLOAD_PATH/$JMETER_DOWNLOAD_FILENAME -C $JMETER_BINARY_PATH
                """
            }
        }
        stage ('Precheck') {
            steps {
                sh """
                    echo $PATH
                    $JMETER_BINARY_PATH/apache-jmeter-5.4.1/bin/jmeter -v
                """
            }
        }
        stage ('Run Betch Test with plugin') {
            steps {
                sh """
                    $JMETER_BINARY_PATH/apache-jmeter-5.4.1/bin/jmeter -n -t $JMETER_JMX_PATH -l $JMETER_RESULT_PATH
                """
            }
        }
        stage ('Fetch Result to perf-plugin') {
            steps {
                perfReport "$JMETER_RESULT_PATH"
            }
        }
   }
}
