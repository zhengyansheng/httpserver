#!/usr/bin/env groovy

@Library('shareLibrary')

//String workspace = "/opt/jenkins/workspace"

// Pipeline
pipeline {
    // 指定运行的节点
    agent any

    tools {
        go 'go124'
    }

    options {
        timestamps()                        // 日志行添加时间
        timeout(time: 30, unit: 'MINUTES')  // build timeout 整个流水线的超时时间
    }

    // 参数
    parameters {
        choice(name: 'action', choices: ['构建', '打包', '发版', '回滚'], description: '操作的指令')
        choice(name: 'branch', choices: ['dev', 'qa', 'uat', 'master'], description: '分支或Tag名称')
        choice(name: 'env', choices: ['dev', 'test', 'test2', 'test3', 'uat', 'prod'], description: '运行的环境')
    }

    // 环境变量
    environment {
        GO114MODULE = 'on'
        CGO_ENABLED = 0
    }

    stages {
        // 执行前的预处理
        stage('pre build') {
            steps {
                script {
                    def startTime = System.currentTimeMillis()
                    writeFile file: 'build_start_time.txt', text: "${startTime}"
                    echo "构建开始时间（毫秒）已记录: ${startTime}"
                }
            }
        }

        // 克隆代码
        stage("git checkout") {
            steps {
                echo "git checkout '${params.branch}'"
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: "*/${params.branch}"]],
                    userRemoteConfigs: [[
                        url: 'https://github.com/zhengyansheng/httpserver',
                    ]]
                ])
            }
        }

        // 构建
        stage("build") {
            steps {
                echo '单元测试'
                sh 'go test ./...'
                sh 'ls -l'
            }
        }

        // 扫描
        stage("scan code") {
            steps {
                echo '扫描代码'
            }
        }

        // 打包和推送
        stage("pack") {
            steps {
                echo '打包推送镜像'
            }
        }

        // 部署
        stage("deploy") {
            steps {
                echo '部署镜像'
                sh 'echo $action, $branch, $env'
            }
        }
    }

   post {
        // currentBuild 全局变量

        always {
            script {
                try {
                    def endTime = System.currentTimeMillis()
                    def startTimeStr = readFile('build_start_time.txt').trim()
                    def startTime = startTimeStr.toLong()
                    def durationMillis = endTime - startTime

                    def seconds = (durationMillis / 1000).toInteger()
                    def minutes = (seconds / 60).toInteger()
                    def remainingSeconds = seconds % 60

                    echo "⏱️ 构建耗时：${minutes} 分 ${remainingSeconds} 秒（共 ${durationMillis} 毫秒）"
                } catch (Exception e) {
                    echo "⚠️ 计算耗时失败: ${e.message}"
                }
            }
        }

        success {
            currentBuild.description += "\n success"
            echo '✅ Pipeline 执行成功！'
        }

        failure {
            currentBuild.description += "\n failure"
            echo '❌ Pipeline 执行失败，请检查日志。'
        }

        aborted {
            currentBuild.description += "\n aborted "
            echo '❌ Pipeline 执行终止，请检查日志。'
        }
   }
}
