
// setBuildDisplayName 设置构建显示的名称
def setBuildDisplayName() {
    // 定义日期时间格式：年-月-日 时:分:秒
    def dateFormat = new java.text.SimpleDateFormat("yyyy-MM-dd HH:mm:ss")
    def currentDateTime = dateFormat.format(new Date())
    def description = currentBuild.displayName + "\n" + "$currentDateTime"
    currentBuild.description = "时间: $currentDateTime" + "\n" + "分支: xx" + "\n" + "环境: xx" + "\n" + "用户: ${env.EXECUTE_JOB_USER_ID}"
}

// CheckoutCode 克隆代码
def checkoutCode(gitUrl, branch) {
    // Clean workspace before checking out code
    deleteDir()
    checkout scmGit(
        // userRemoteConfigs: [[credentialsId:  'git_pull_secret', url: gitUrl]],
        userRemoteConfigs: [[url: gitUrl]],
        branches: [[name: branch]]
    )
}



// 流水线
pipeline {

    // 执行的节点
    agent any

    // 参数
    parameters {
        choice(name: 'action', choices: ['构建', '打包', '部署', '回滚'], description: '操作的指令')
        choice(name: 'branch', choices: ['dev', 'qa', 'uat', 'master', 'main'], description: '分支或Tag名称')
//         choice(name: 'env', choices: ['dev', 'test', 'test2', 'test3', 'uat', 'prod'], description: '运行的环境')
//         choice(name: 'codeType', choices: ['java', 'nodejs', 'common', 'go', 'python'], description: '代码类型')
    }

    // 阶段
    stages {
        stage('初始化/ initialization') {
            steps {
                echo '初始化'
                
                wrap([$class: 'BuildUser']) {
                    script {
                        echo "触发用户ID: ${env.BUILD_USER_ID}"      // 如 'admin'
                        env.EXECUTE_JOB_USER_ID = "${env.BUILD_USER_ID}"
                    }
                }
                
                script {

                    setBuildDisplayName()

                }
            }
        }

        stage('检出代码/ checkout code') {
            steps {
                echo '检出代码'
                
                script {
                
                    println("checkout code")
//                     checkoutCode()
                    
                }
            }
        }

        stage('编译/ build') {
            steps {
                echo '编译'

                script {

                    println("build")

                }
            }
        }

        stage('构建和推送镜像/ build and push image') {
            steps {
                echo '构建和推送镜像'

                script {

                    println("build and push image")

                }
            }
        }
        
        stage('部署/ deployment') {
            steps {
                echo '部署'

                script {

                    println("deployment")

                }
            }
        }

    }

    // 钩子
    post {
      always {
            script {
                println("job执行结束")
            }
      }
      aborted {
            script {
                println("job终止")
            }
      }
      success {
            script {
                println("job执行成功")
            }
      }
      failure {
            script {
                println("job执行失败")
            }
      }
    }


}
