//@Library('Utils') _ //vars/getUser.groovy
pipeline {
    // min hour day/month day/year day/week 
    // frequency */15 
    // range 1-2
    // random H H(1-2) H/15
    // triggers { cron (15 * * * * *)}

    // 轮询扫描SCM变更 软件配置管理(SCM)
    // triggers{ polSCM(*/20 * * * *)}

    // @yearly * * * H *
    // @annually @monthly @weekly @daily @midnight @hourly


    agent {label 'master'}

    properties ([
        parameters {
        // echo ${params.USERID}
            string(name: 'USERID', defaultValue: '',
                description: 'Enter your userid')
        }
    ])

    stages {
        stage('Name') {
            // 脚本式
            steps {
                //script {
                    //def answer = input messag: '<message>', parameters: [booleanParam (defaultValue: true,
                    //description: 'Prerelease setting', name: 'prerelease')]

                    //def choice = input message: '<message>', 
                        //parameters: [choice (choices: "choice1\nchoice2\nchoice3\n",
                        //description: 'Choose an option', name: 'Options')]

                    // BlueOcean 不支持文件输入 
                    // def selectedFile = input message: '<message>',
                        // parameters: [file(description: 'Choose file to upload', name: 'local')]
                //}
                timeout(time: 20, unit:'SECONDS') {
                    git 'https://github.com/rainfd/devops-examples'
                }

                // retry(1) {}

                // sleep time: 5, unit: 'MINUTES'

                // timeout() {
                    //waitUtil { 
                        //try {}   
                        //catch (exception) {}
                        //return true 
                    //}
                //}
                // 
                // lock('master', quantity: 1) { }
            }


            // 并行
            // script {
            //     def stepsToRun = [:]
            //     for (int i = 1; i < 5; i++) {
            //         stepsToRun["Step${i}"] = { node {
            //             echo "start" sleep 5
            //         }}
            //     }
            //     parallel stepsToRun
            // }
        }

        // 其他构建到达这步时就会被取消
        milestone label: 'After build', ordinal 1
    }

    parallel {
        stage('One') {
            agent { label 'master' }
            steps {
                // 总是运行一个新的工作空间
                cleanWs()
                stash name: "xx-package", includes: 'build.'
            }
        }
        stage('Tow') {
            agent { label 'xx' }
            steps {
                cleanWs()
                unstash 'xx-pakcage'
            }
        }
    }

    stages {
        stage() {
            steps {
                parallel (
                    'xx': {},
                    'xx2': {}
                )
            }
        }
    }
}