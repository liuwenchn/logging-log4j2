#!groovy
/*
 * Licensed to the Apache Software Foundation (ASF) under one or more
 * contributor license agreements.  See the NOTICE file distributed with
 * this work for additional information regarding copyright ownership.
 * The ASF licenses this file to You under the Apache License, Version 2.0
 * (the "License"); you may not use this file except in compliance with
 * the License.  You may obtain a copy of the License at
 *
 *     https://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

pipeline {
    agent {
        label 'ubuntu&&!H20'
    }
    tools {
        jdk 'JDK 1.8 (latest)'
        maven 'Maven 3 (latest)'
    }
    stages {
        stage('Build') {
            steps {
                ansiColor('xterm') {
                    sh 'mvn -t jenkins-toolchains.xml -Djenkins -DskipTests=true -Dmaven.javadoc.skip=true -V install'
                    sh 'mvn -t jenkins-toolchains.xml -Djenkins -V install'
                }
            }
        }
        stage('Deploy') {
            when { branch 'master' }
            steps {
                ansiColor('xterm') {
                    sh 'mvn -t jenkins-toolchains.xml -Djenkins -V deploy'
                }
            }
//            post {
//                failure {
//                    emailext body: "See <${env.BUILD_URL}>", replyTo: 'dev@logging.apache.org', subject: "[Log4j] Jenkins build failure (#${env.BUILD_NUMBER})", to: 'notifications@logging.apache.org'
//                }
//            }
        }
    }
}
